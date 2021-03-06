# Release Train Issue Template for Alpakka

(Liberally copied and adopted from Scala itself https://github.com/scala/scala-dev/blob/b11cd2e4a4431de7867db6b39362bea8fa6650e7/notes/releases/template.md)

For every Alpakka release, make a copy of this file named after the release, and expand the variables.
Ideally replacing variables could become a script you can run on your local machine.

Variables to be expanded in this template:
- $ALPAKKA_VERSION$=??? 

Key links:
  - akka/alpakka milestone: https://github.com/akka/alpakka/milestone/?

### ~ 1 week before the release

- [ ] Check that any new `deprecated` annotations use the correct version name
- [ ] Check that open PRs and issues assigned to the milestone are reasonable
- [ ] Decide on planned release date
- [ ] Notify depending projects (Akka persistence plugins) about the upcoming release
- [ ] Create a new milestone for the [next version](https://github.com/akka/alpakka/milestones)
- [ ] Check [closed issues without a milestone](https://github.com/akka/alpakka/issues?utf8=%E2%9C%93&q=is%3Aissue%20is%3Aclosed%20no%3Amilestone) and either assign them the 'upcoming' release milestone or `invalid/not release-bound`

### 1 day before the release

- [ ] Make sure all important / big PRs have been merged by now
- [ ] Communicate that a new version is about to be released in [Gitter Akka Dev Channel](https://gitter.im/akka/dev), so that no new Pull Requests are merged

### Preparing release notes in the documentation / announcement

- [ ] If this is a new minor (not patch) release, rename the 'alpakka-x.x-stable' and 'alpakka-supported-x.x-stable' reporting projects in [WhiteSource](https://saas.whitesourcesoftware.com/Wss/WSS.html#!project;id=517292) accordingly (unfortunately this requires permissions that cannot be shared outside of Lightbend)
- [ ] Add a release notes entry in `docs/src/main/paradox/release-notes/` listing contributors generated by [`sbt-authors`](https://github.com/2m/authors) (eg. `sbt authors v0.22 HEAD`)
- [ ] Create a news item draft PR on [akka.github.com](https://github.com/akka/akka.github.com), using the milestone
- [ ] Move all [unclosed issues](https://github.com/akka/alpakka/issues?q=is%3Aopen+is%3Aissue+milestone%3A$ALPAKKA_VERSION$) for this milestone to the next milestone
- [ ] Release notes PR has been merged

### Cutting the release

- [ ] Make sure there are no stray staging repos on [Sonatype](https://oss.sonatype.org/#stagingRepositories)
- [ ] Wait until [master build finished](https://travis-ci.org/akka/alpakka/builds/) after merging the release notes 
- [ ] Create a [new release](https://github.com/akka/alpakka/releases/new) with the next tag version `v$ALPAKKA_VERSION$`, title and release description linking to announcement, release notes and milestone
- [ ] Check that Travis CI release build has executed successfully (Travis will start a [CI build](https://travis-ci.org/akka/alpakka/builds) for the new tag and publish artifacts to Bintray and documentation to Gustav)
- [ ] Go to [Bintray](https://bintray.com/akka/maven/alpakka) and select the just released version
- [ ] Go to the Maven Central tab and sync with Sonatype (using your Sonatype TOKEN key and password)
- [ ] Log in to Sonatype to close the staging repository (optional, should happen automatically if selected in Bintray)
- [ ] Release the staging repository to Maven Central

### Check availability

- [ ] Check release on [Sonatype](https://oss.sonatype.org/content/repositories/releases/com/lightbend/akka/akka-stream-alpakka-xml_2.12/$ALPAKKA_VERSION$/)
- [ ] Check the release on [Maven central](http://central.maven.org/maven2/com/lightbend/akka/akka-stream-alpakka-xml_2.12/$ALPAKKA_VERSION$/)

### Announcements

- [ ] Merge draft news item for [akka.io](https://github.com/akka/akka.github.com)
- [ ] Send a release notification to [Lightbend discuss](https://discuss.akka.io)
- [ ] Tweet using the akkateam account (or ask someone to) about the new release
- [ ] Announce on [Gitter akka/akka](https://gitter.im/akka/akka)

### Afterwards

- [ ] If Cassandra has relevant changes, create/update PR in [Akka Persistence Cassandra](https://github.com/akka/akka-persistence-cassandra/) to upgrade to $ALPAKKA_VERSION$
- [ ] If Couchbase has relevant changes, create/update PR in [Akka Persistence Couchbase](https://github.com/akka/akka-persistence-couchbase/) to upgrade to $ALPAKKA_VERSION$
- [ ] Update version for [Lightbend Supported Modules](https://developer.lightbend.com/docs/reactive-platform/2.0/supported-modules/#other-akka-modules) in [private project](https://github.com/lightbend/reactive-platform-docs/blob/master/build.sbt#L77)
- [ ] Close the [$ALPAKKA_VERSION$ milestone](https://github.com/akka/alpakka/milestones?direction=asc&sort=due_date)
- Close this issue
