# Ginkgo
some notes about Ginkgo:
 You use Describe blocks to describe the individual behaviors of your code and Context blocks to exercise those behaviors under different circumstances
 The above example illustrates a common antipattern in BDD-style testing. Our top level BeforeEach creates a new book using valid JSON, but a lower level Context exercises the case where a book is created with invalid JSON. This causes us to recreate and override the original book. Thankfully, with Ginkgo’s JustBeforeEach blocks, this code duplication is unnecessary.

JustBeforeEach blocks are guaranteed to be run after all the BeforeEach blocks have run and just before the It block has run. We can use this fact to clean up the Book specs:
