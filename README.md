Running `./gradlew clean testDebugUnitTest` has the following results:

* With robolectric 3.8:
```
java.lang.NumberFormatException: For input string: "@integer/port"

	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:65)
	at java.lang.Integer.parseInt(Integer.java:580)
	at java.lang.Integer.parseInt(Integer.java:615)
	at android.content.IntentFilter$AuthorityEntry.__constructor__(IntentFilter.java:904)
	at android.content.IntentFilter$AuthorityEntry.<init>(IntentFilter.java)
	at android.content.IntentFilter.addDataAuthority(IntentFilter.java:1108)
	at org.robolectric.shadows.LegacyManifestParser.populateIntentInfo(LegacyManifestParser.java:338)
	at org.robolectric.shadows.LegacyManifestParser.createPackage(LegacyManifestParser.java:245)
	at org.robolectric.android.internal.ParallelUniverse.setUpApplicationState(ParallelUniverse.java:122)
	at org.robolectric.RobolectricTestRunner.beforeTest(RobolectricTestRunner.java:335)
	at org.robolectric.internal.SandboxTestRunner$2.evaluate(SandboxTestRunner.java:245)
	at org.robolectric.internal.SandboxTestRunner.runChild(SandboxTestRunner.java:130)
	at org.robolectric.internal.SandboxTestRunner.runChild(SandboxTestRunner.java:42)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
	at org.robolectric.internal.SandboxTestRunner$1.evaluate(SandboxTestRunner.java:84)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
	at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
	at com.intellij.junit4.JUnit4IdeaTestRunner.startRunnerWithArgs(JUnit4IdeaTestRunner.java:68)
	at com.intellij.rt.execution.junit.IdeaTestRunner$Repeater.startRunnerWithArgs(IdeaTestRunner.java:47)
	at com.intellij.rt.execution.junit.JUnitStarter.prepareStreamsAndStart(JUnitStarter.java:242)
	at com.intellij.rt.execution.junit.JUnitStarter.main(JUnitStarter.java:70)
	at com.intellij.rt.execution.application.AppMainV2.main(AppMainV2.java:131)
```

* With robolectric 3.8 and this workaround:
```
tasks.withType(Test) {
    // Uncomment the following to make tests pass on robolectric 3.8
    jvmArgs("-Duse_framework_manifest_parser=true")
}
```
Tests pass

* With robolectric 4.0-alpha-3:
```
java.lang.NumberFormatException: For input string: "@integer/port"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:65)
	at java.lang.Integer.parseInt(Integer.java:580)
	at java.lang.Integer.parseInt(Integer.java:615)
	at android.content.IntentFilter$AuthorityEntry.__constructor__(IntentFilter.java:904)
	at android.content.IntentFilter$AuthorityEntry.<init>(IntentFilter.java)
	at android.content.IntentFilter.addDataAuthority(IntentFilter.java:1108)
	at org.robolectric.shadows.LegacyManifestParser.populateIntentInfo(LegacyManifestParser.java:350)
	at org.robolectric.shadows.LegacyManifestParser.createPackage(LegacyManifestParser.java:247)
	at org.robolectric.android.internal.ParallelUniverse.setUpApplicationState(ParallelUniverse.java:126)
	at org.robolectric.RobolectricTestRunner.beforeTest(RobolectricTestRunner.java:392)
	at org.robolectric.internal.SandboxTestRunner$2.evaluate(SandboxTestRunner.java:252)
	at org.robolectric.internal.SandboxTestRunner.runChild(SandboxTestRunner.java:130)
	at org.robolectric.internal.SandboxTestRunner.runChild(SandboxTestRunner.java:42)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
	at org.robolectric.internal.SandboxTestRunner$1.evaluate(SandboxTestRunner.java:84)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
```

* With robolectric 4.0-alpha-3 and the `use_framework_manifest_parser` workaround:
Same result as without the workaround: this propertly is no longer read:
```
java.lang.NumberFormatException: For input string: "@integer/port"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:65)
	at java.lang.Integer.parseInt(Integer.java:580)
	at java.lang.Integer.parseInt(Integer.java:615)
	at android.content.IntentFilter$AuthorityEntry.__constructor__(IntentFilter.java:904)
	at android.content.IntentFilter$AuthorityEntry.<init>(IntentFilter.java)
	at android.content.IntentFilter.addDataAuthority(IntentFilter.java:1108)
	at org.robolectric.shadows.LegacyManifestParser.populateIntentInfo(LegacyManifestParser.java:350)
	at org.robolectric.shadows.LegacyManifestParser.createPackage(LegacyManifestParser.java:247)
	at org.robolectric.android.internal.ParallelUniverse.setUpApplicationState(ParallelUniverse.java:126)
	at org.robolectric.RobolectricTestRunner.beforeTest(RobolectricTestRunner.java:392)
	at org.robolectric.internal.SandboxTestRunner$2.evaluate(SandboxTestRunner.java:252)
	at org.robolectric.internal.SandboxTestRunner.runChild(SandboxTestRunner.java:130)
	at org.robolectric.internal.SandboxTestRunner.runChild(SandboxTestRunner.java:42)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
	at org.robolectric.internal.SandboxTestRunner$1.evaluate(SandboxTestRunner.java:84)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
```
