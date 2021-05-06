---
layout: post
title: "Bloom Filter (Rust)"
date: 2020-07-20 13:01:20 +0300
description: Bloom Filter in Rust . # Add post description (optional)
img:  rust101.png # Add image post (optional)
categories: rust-language
icon: blogging.png
---

### Applications of bloom filter
- Weak password detection
- Internet Cache Protocol
- Safe browsing in Google Chrome
- Wallet synchronization in Bitcoin
- Hash based IP Traceback
- In Cyber-security like virus scanning
- Prevent your users from accessing malicious sites.
- Instead of making a query to an SQL database to check if a user with a certain email exists, you could first use a bloom filter for an inexpensive lookup check. If the email doesn’t exist, great! If it does exist, you might have to make an extra query to the database. You can do the same to search for if a ‘Username is already taken’.
- IP address of the visitors to your website to check if a user to your website is a ‘returning user’ or a ‘new user’. Some false positive value for ‘returning user’ won’t hurt you, right?
- Spell-checker by using bloom filter to track the dictionary words.
- Want to know how Medium used bloom filter to decide if a user already read post? Read this mind-blowing, freaking awesome article about it.
- prevent your users from accessing malicious sites.
- Instead of making a query to an SQL database to check if a user with a certain email exists, you could first use a bloom filter for an inexpensive lookup check. If the email doesn’t exist, great! If it does exist, you might have to make an extra query to the database. You can do the same to search for if a ‘Username is already taken’.
- IP address of the visitors to your website to check if a user to your website is a ‘returning user’ or a ‘new user’. Some false positive value for ‘returning user’ won’t hurt you, right?
- Spell-checker by using bloom filter to track the dictionary words.
- Want to know how Medium used bloom filter to decide if a user already read post? Read this mind-blowing, freaking awesome article about it.

### Extensions and applications
- Cache filtering
- Avoiding false positives in a finite universe
- Counting Bloom filters
- Decentralized aggregation
- Distributed Bloom filters
- Data synchronization
- Bloomier filters
- Compact approximators
- Parallel Partitioned Bloom Filters
- Stable Bloom filters
- Scalable Bloom filters
- Spatial Bloom filters
- Layered Bloom filters
- Attenuated Bloom filters
- Chemical structure searching

### Code

```rust
extern crate bit_vec;

use bit_vec::BitVec;
use std::collections::hash_map::{DefaultHasher, RandomState};
use std::hash::{BuildHasher, Hash, Hasher};
use std::marker::PhantomData;

#[doc(inline)]
pub struct StandardBloomFilter<T: ?Sized> {
    bitmap: BitVec,
    /// Size of the bit array.
    optimal_m: usize,
    /// Number of hash functions.
    optimal_k: u32,
    /// Two hash functions from which k number of hashes are derived.
    hashers: [DefaultHasher; 2],
    _marker: PhantomData<T>,
}

impl<T: ?Sized> StandardBloomFilter<T> {
    /// Create a new StandardBloomFilter that expects to store `items_count`
    /// membership with a false positive rate of the value specified in `fp_rate`.
    pub fn new(items_count: usize, fp_rate: f64) -> Self {
        let optimal_m = Self::bitmap_size(items_count, fp_rate);
        let optimal_k = Self::optimal_k(fp_rate);
        let hashers = [
            RandomState::new().build_hasher(),
            RandomState::new().build_hasher(),
        ];
        StandardBloomFilter {
            bitmap: BitVec::from_elem(optimal_m as usize, false),
            optimal_m,
            optimal_k,
            hashers,
            _marker: PhantomData,
        }
    }

    /// Insert item to the set.
    pub fn insert(&mut self, item: &T)
    where
        T: Hash,
    {
        let (h1, h2) = self.hash_kernel(item);

        for k_i in 0..self.optimal_k {
            let index = self.get_index(h1, h2, k_i as u64);

            self.bitmap.set(index, true);
        }
    }

    /// Check if an item is present in the set.
    /// There can be false positives, but no false negatives.
    pub fn contains(&mut self, item: &T) -> bool
    where
        T: Hash,
    {
        let (h1, h2) = self.hash_kernel(item);

        for k_i in 0..self.optimal_k {
            let index = self.get_index(h1, h2, k_i as u64);

            if !self.bitmap.get(index).unwrap() {
                return false;
            }
        }

        true
    }

    /// Get the index from hash value of `k_i`.
    fn get_index(&self, h1: u64, h2: u64, k_i: u64) -> usize {
        h1.wrapping_add((k_i).wrapping_mul(h2)) as usize % self.optimal_m
    }

    /// Calculate the size of `bitmap`.
    /// The size of bitmap depends on the target false positive probability
    /// and the number of items in the set.
    fn bitmap_size(items_count: usize, fp_rate: f64) -> usize {
        let ln2_2 = core::f64::consts::LN_2 * core::f64::consts::LN_2;
        ((-1.0f64 * items_count as f64 * fp_rate.ln()) / ln2_2).ceil() as usize
    }

    /// Calculate the number of hash functions.
    /// The required number of hash functions only depends on the target
    /// false positive probability.
    fn optimal_k(fp_rate: f64) -> u32 {
        ((-1.0f64 * fp_rate.ln()) / core::f64::consts::LN_2).ceil() as u32
    }

    /// Calculate two hash values from which the k hashes are derived.
    fn hash_kernel(&self, item: &T) -> (u64, u64)
    where
        T: Hash,
    {
        let hasher1 = &mut self.hashers[0].clone();
        let hasher2 = &mut self.hashers[1].clone();

        item.hash(hasher1);
        item.hash(hasher2);

        let hash1 = hasher1.finish();
        let hash2 = hasher2.finish();

        (hash1, hash2)
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn insert() {
        let mut bloom = StandardBloomFilter::new(100, 0.01);
        bloom.insert("item");
        assert!(bloom.contains("item"));
    }

    #[test]
    fn check_and_insert() {
        let mut bloom = StandardBloomFilter::new(100, 0.01);
        assert!(!bloom.contains("item_1"));
        assert!(!bloom.contains("item_2"));
        bloom.insert("item_1");
        assert!(bloom.contains("item_1"));
        assert!(!bloom.contains("item_2"));
    }
}
```