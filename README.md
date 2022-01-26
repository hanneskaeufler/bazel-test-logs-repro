1. Run `bazel test //...`
   you will see a failed and a passed test:

```
INFO: Analyzed 2 targets (1 packages loaded, 4 targets configured).
INFO: Found 2 test targets...
FAIL: //:fails (see /private/var/tmp/_bazel_hanneskaeufler/99b111e2b3ab5266e48d79afc950337e/execroot/__main__/bazel-out/darwin_arm64-fastbuild/testlogs/fails/test.log)
INFO: Elapsed time: 0,396s, Critical Path: 0,30s
INFO: 2 processes: 2 darwin-sandbox.
INFO: Build completed, 1 test FAILED, 2 total actions
//:passes                                                       (cached) PASSED in 0.5s
//:fails                                                                 FAILED in 0.3s
  /private/var/tmp/_bazel_hanneskaeufler/99b111e2b3ab5266e48d79afc950337e/execroot/__main__/bazel-out/darwin_arm64-fastbuild/testlogs/fails/test.log

Executed 1 out of 2 tests: 1 test passes and 1 fails locally.
INFO: Build completed, 1 test FAILED, 2 total actions
```

2. Look for test.xml in output: `find bazel-testlogs/ -name '*.xml'`
   You will see two xmls for the two respective tests

```
bazel-testlogs//passes/test.xml
bazel-testlogs//fails/test.xml
```

3. Comment the failing test, like in the following diff:

```diff
-sh_test(
-    name = "fails",
-    srcs = ["fails.sh"],
-)
+# sh_test(
+#     name = "fails",
+#     srcs = ["fails.sh"],
+# )
```

4. Run the tests again `bazel test //...`

```
INFO: Analyzed target //:passes (1 packages loaded, 2 targets configured).
INFO: Found 1 test target...
Target //:passes up-to-date:
  bazel-bin/passes
INFO: Elapsed time: 0,134s, Critical Path: 0,00s
INFO: 1 process: 1 internal.
INFO: Build completed successfully, 1 total action
//:passes                                                       (cached) PASSED in 0.5s

Executed 0 out of 1 test: 1 test passes.
INFO: Build completed successfully, 1 total action
```

5. Look for test xmls again `find bazel-testlogs/ -name '*.xml'`

```
find bazel-testlogs/ -name '*.xml'
bazel-testlogs//passes/test.xml
bazel-testlogs//fails/test.xml
```

**I do not expect to see fails/test.xml there**
