# Ginkgo
some notes about Ginkgo: http://onsi.github.io/ginkgo
 You use Describe blocks to describe the individual behaviors of your code and Context blocks to exercise those behaviors under different circumstances
 The above example illustrates a common antipattern in BDD-style testing. Our top level BeforeEach creates a new book using valid JSON, but a lower level Context exercises the case where a book is created with invalid JSON. This causes us to recreate and override the original book. Thankfully, with Ginkgo’s JustBeforeEach blocks, this code duplication is unnecessary.

JustBeforeEach blocks are guaranteed to be run after all the BeforeEach blocks have run and just before the It block has run. We can use this fact to clean up the Book specs:
## Spec Runner
1.Focused spec doing so instructs Ginkgo to only run those specs. To run all specs, you’ll need to go back and remove all the Fs.
skip spec x and  p
2.You can pass in a regular expression with the --focus=REGEXP and/or --skip=REGEXP flags. Ginkgo will only run specs that match the focus regular expression and don’t match the skip regular expression.

3.In cases where specs dont provide enough hierarchichal distinction between groups of tests, directories can be included in the matching of focus and skip, via the --regexScansFilePath option. 
It is sometimes necessary/preferable to view the output of the individual parallel test suites in real-time. To do this you can set -stream:

ginkgo -nodes=N -stream

The idea here is simple. With SynchronizedBeforeSuite Ginkgo gives you a way to run some preliminary setup code on just one parallel node (Node 1) and other setup code on all nodes. Ginkgo synchronizes these functions and guarantees that node 1 will complete its preliminary setup before the other nodes run their setup code.

## Precompiling tests

Ginkgo has strong support for writing integration-style acceptance tests. These tests are useful tools to validate that (for example) a complex distributed system is functioning correctly. It is often convenient to distribute these acceptance tests as standalone binaries.

Ginkgo allows you to build such binaries with:

```ginkgo build path/to/package```

## Benchmark
 Measure blocks can go wherever an It block can go – each Measure generates a new spec. The closure function passed to Measure must take a Benchmarker argument. The Benchmarker is used to measure runtimes and record arbitrary numerical values. You must also pass Measure an integer after your closure function, this represents the number of samples of your code Measure will perform.
## Table Driven tests
The table provides an expressive DSL for writing table driven tests.
The function you pass in to DescribeTable can accept arbitrary arguments. The parameters passed in to the individual Entry calls will be passed in to the function (type mismatches will result in a runtime panic).

The indiviudal Entry calls construct a TableEntry that is passed into DescribeTable. A TableEntry consists of a description (the first call to Entry) and an arbitrary set of parameters to be passed into the function registered with DescribeTable.

It’s important to understand the life-cycle of the table. The table package is a thin wrapper around Ginkgo’s DSL. DescribeTable generates a single Ginkgo Describe, within this Describe each Entry generates a Ginkgo It. This all happens before the tests run (at “testing tree construction time”). The result is that the table expands into a number of Its (one for each Entry) that are subject to all of Ginkgo’s test-running semantics: Its can be randomized and parallelized across multiple nodes.
## Writing custom reporters
```type Reporter interface {
    SpecSuiteWillBegin(config config.GinkgoConfigType, summary *types.SuiteSummary)
    BeforeSuiteDidRun(setupSummary *types.SetupSummary)
    SpecWillRun(specSummary *types.SpecSummary)
    SpecDidComplete(specSummary *types.SpecSummary)
    AfterSuiteDidRun(setupSummary *types.SetupSummary)
    SpecSuiteDidEnd(summary *types.SuiteSummary)
}```
