---
layout: post
title: "Release Management With Git"
date: 2016-11-24 16:25:06 -0500
comments: true
---

Git makes distributed software development easy. Especially Release Management!

Just merge the branch that's currently being worked on (usually develop) into a release branch (usually master), tag it, and your'e done. The CI tool is configured to pull off the master branch's tagged commit and there's your release.

Time passes and you do this again, possibly with the next sprint.

Where it gets a little tedious is when you are asked: What are the new features added in a certain release. Would it not be great if this data was automatically generated without someone having to check the git log or scrutinize the commit graph in SourceTree?

So here's a neat solution.. With a bit of discipline in your team and the use a nifty maven plugin, you can have release notes generated automatically as a JSON file that can then be (optionally) exposed via a web interface.

#### First, the rules:

* You have to be using a [Git](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics) repository for Source Control.
* You must be using a standard [gitflow](http://nvie.com/posts/a-successful-git-branching-model/). This is one that works well.
* You must be using [Maven](https://maven.apache.org/what-is-maven.html) for the build of your project
* You must use the maven-commit-id-plugin


#### Next, the discipline :

Git is a branch-often-commit-often DVCS. That is a great idea for development; after all, developers may want to reset to a previous commit, try something experimental in a sub-branch or just share a commit with a co-worker.

But these commits are not very meaningful as release notes:

For example:

* Fixed tests
* Added exception
* Refactored code
* wip :)

.. will not make great release notes!

#### To address this explosion of commits, there are 2 options:

1. When code is being submitted for a Pull Request, insist that developers squash commits on the feature branch into one 
or two meaningful commits that represent the change or feature.
1. The person who is merging/accepting the Pull Request, either creates another commit  that represents the change, or amends an existing commit(s)  (on the feature branch), with a token (say the ticket number) in the commit message. This token will tell the maven plugin which commit message to include in the release notes, and which to ignore.
With the above in place, the feature branch can be merged into the develop branch.

When the release needs to be cut, the develop branch is merged into master (say) and suitably tagged with a release label like R_1.3.0.

For the next release, the process is repeated and a label like R_1.3.1 is created.

Now, configure your project to use the releaseNotes goal of the maven-git-commit-id plugin. By configuring the plugin to pick up release notes between startTag - R_1.3.1 and endTag - R_1.3.0, we will be able to produce a JSON file with the release notes extracted from the commit messages as described above.

#### Here is an example:

**Given** a backlog in your _Save The World_ (STW) project that looks like below:

* STW-101: Plant some trees
* STW-102: Feed the hungry
* STW-103: Save the whales
* STW-104: Bike to work
* STW-105: Eat some veggies
* STW-107: Meditate and cogitate
* STW-108: Gaze at the night sky
* STW-109: Do 21 days of Yoga
* STW-110: Express my gratitude
* STW-113: Write a helpful blogpost
* STW-114: Contribute to the open source community
* STW-115: Dream more
* STW-116: Eat less
* STW-117: Worry less
* STW-118: Plan less


**When** the developers have done some work, here is what the commit graph may end up looking like:

<p align="center">
  <img src="{{ site.baseurl}}/images/commit-graph.png" width="800" height="600"/>
</p>


And your project pom is configured like so:

```
...
<plugin>
    <groupId>pl.project13.maven</groupId>
    <artifactId>git-commit-id-plugin</artifactId>
    <version>2.2.2-SNAPSHOT</version>
    <executions>
        <execution>
            <id>releaseNotes</id>
            <goals>
                <goal>releaseNotes</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <dotGitDirectory>${project.basedir}/.git</dotGitDirectory>
        <tagNameRegex>R_[0-9].[0-9].[0-9].*</tagNameRegex>
        <commitMessageRegex>STW-[0-9][0-9][0-9]</commitMessageRegex>
        <releaseNotesFileName>${project.basedir}/src/main/webapps/rel-notes.json</releaseNotesFileName>
    </configuration>
</plugin>
 ...           
```

**Then** the above commit graph will produce a JSON below:

```
{  
   "generationTime":"2016/11/24 18:15:54 EST",
   "startTag":"R_1.0.1",
   "endTag":null,
   "commitMessageRegex":"STW-[0-9][0-9][0-9]",
   "tagNameRegex":"R_[0-9].[0-9].[0-9].*",
   "tagList":[  
      {  
         "name":"refs/tags/R_1.0.1",
         "featureList":[  
            {  
               "description":"STW-109 Done with Yoga\n",
               "commitHashShort":"a49d034",
               "commitHashLong":"a49d034adbc0f8d517d7841853bd691cc616dc08",
               "author":"Ben Rothlisberger",
               "commitTime":"2016/11/24 18:06:43 EST"
            },
            {  
               "description":"STW-101 Done planting trees\n",
               "commitHashShort":"5287516",
               "commitHashLong":"528751680aea6685eb56b083c232da72c3870291",
               "author":"Antonio Brown",
               "commitTime":"2016/11/24 18:06:37 EST"
            }
         ]
      },
      {  
         "name":"refs/tags/R_1.0.0",
         "featureList":[  
            {  
               "description":"STW-117 Done worrying\n",
               "commitHashShort":"765a35a",
               "commitHashLong":"765a35a91aa9bc558b77e5de1c78f00a487b4ca4",
               "author":"Hines Ward",
               "commitTime":"2016/11/24 18:06:31 EST"
            },
            {  
               "description":"STW-116 Done eating!\n",
               "commitHashShort":"8b88104",
               "commitHashLong":"8b88104c22415acdcd57c802c09c1894848f4618",
               "author":"Hines Ward",
               "commitTime":"2016/11/24 18:06:26 EST"
            },
            {  
               "description":"STW-118 Done planning\n",
               "commitHashShort":"374e860",
               "commitHashLong":"374e860ed6fae44e7f16ace28e529cc243db8e02",
               "author":"Antonio Brown",
               "commitTime":"2016/11/24 18:06:21 EST"
            },
            {  
               "description":"STW-115 Done dreaming!\n",
               "commitHashShort":"5d1a577",
               "commitHashLong":"5d1a577b212e0eae75b01aca70a606874b439a0a",
               "author":"Leveon Bell",
               "commitTime":"2016/11/24 18:05:59 EST"
            }
         ]
      }
   ]
}
```

Notice that the release notes have picked up only those commit messages that match the commit message regular expression (STW-[0-9][0-9][0-9]).
Also, the commit's are nicely separated by release tags, so your users can not only see the most recent releases but also the earlier ones.

And now, all that's left to do is expose this JSON in your UI!

