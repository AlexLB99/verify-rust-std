# Challenge XXXX[^challenge_id]: Verify reference-counted Cell implementation

- **Status:** Open
- **Solution:** *Option field to point to the PR that solved this challenge.*
- **Tracking Issue:** *Link to issue*
- **Start date:** 2025/05/01
- **End date:** 2025/12/31
- **Reward:** *TBD*[^reward]

-------------------


## Goal

The goal of this challenge is to verify the Rc and Arc implementations. Rc and Arc are the library-provided building blocks that enable safe multiple ownership of data through reference counting. This challenge will yield 

This challenge will not address the Weak implementation and the parts of Rc that deal with Weak; we will leave those for a future challenge.

## Motivation

The Rc (for single-threaded code) and Arc (atomic multi-threaded) types are widely used in Rust programs to enable shared ownership of data through reference counting. Since shared ownership is generally not permitted by Rust's type system, these implementations use unsafe code to bypass Rust's usual compile-time checks. Verifying the Rust standard library thus fundamentally requires verification of these types.

The verification includes verification of a number of Rc and Arc methods that encapsulate unsafety, as well as providing contracts for unsafe methods that impose safety conditions on their callers for correct use.

## Description

*Describe the challenge in more details.*

### Assumptions

*Mention any assumption that users may make. Example, "assuming the usage of Stacked Borrows".*

### Success Criteria

All the following unsafe functions must be annotated with safety contracts and the contracts have been verified:

| Function | Location |
|---------|---------|
|  Rc<mem::MaybeUninit<T>,A>::assume_init   |  alloc::rc    |
|  Rc<[mem::MaybeUninit<T>],A>::assume_init   |  alloc::rc    |
|  Rc<T>::from_raw  | alloc::rc |
|  Rc<T>::from_raw_in  | alloc::rc |
|  Rc<T>::increment_strong_count  | alloc::rc |
|  Rc<T>::increment_strong_count_in  | alloc::rc |
|  Rc<T>::decrement_strong_count  | alloc::rc |
|  Rc<T>::decrement_strong_count_in  | alloc::rc |
|  Rc<T>::get_mut_unchecked | alloc::rc | 
|  Rc<T>::downcast_unchecked | alloc::rc |
|  Arc<mem::MaybeUninit<T>,A>::assume_init   |  alloc::sync    |
|  Arc<[mem::MaybeUninit<T>],A>::assume_init   |  alloc::sync    |
|  Arc<T>::from_raw  | alloc::sync |
|  Arc<T>::from_raw_in  | alloc::sync |
|  Arc<T>::increment_strong_count  | alloc::sync |
|  Arc<T>::increment_strong_count_in  | alloc::sync |
|  Arc<T>::decrement_strong_count  | alloc::sync |
|  Arc<T>::decrement_strong_count_in  | alloc::sync |
|  Arc<T>::get_mut_unchecked | alloc::sync | 
|  Arc<T>::downcast_unchecked | alloc::sync |

At least N of the following usages were proven safe:

| Function | Location |
|---------|---------|
|  xyz   |  123   |

All proofs must automatically ensure the absence of the following undefined behaviors [ref](https://github.com/rust-lang/reference/blob/142b2ed77d33f37a9973772bd95e6144ed9dce43/src/behavior-considered-undefined.md):

*List of UBs*

Note: All solutions to verification challenges need to satisfy the criteria established in the [challenge book](general-rules.md)
in addition to the ones listed above.

[^challenge_id]: The number of the challenge sorted by publication date.
[^reward]: Leave it as TBD when creating a new challenge. This should only be filled by the reward committee.
