# doCMent
As a software engineer I want a way for members of my team to create and manage documentation in my CM repository so that I can treat documents just like software in my processes.

This originally started as an idea to help non-Devs utilize good CM practices for thier document oriented workflows.  While I still believe that is important, there are considerable documentation challenges associated with development teams and it is equally important to address those.  While this may evolve over time to enable non-Devs, I'm choosing to start with a Dev-centric approach leveraging their comfort with text-based work products, CM, and automation.  Assuming this shows sufficient promise, I'll consider features or perhaps a fork to better support non-Devs.

Previously I've explored the concept of a [Document Pipeline](https://github.com/jondavid-black/Doc_Pipeline).  While this did work and produced good output, it was a bit complex and required an environment be put in place that was not defined in the CM baseline.  It was also completely focused on a single document which may not be practical for teams as they must maintain documentation for design, test, or other aspects of their product.  While I may choose to utilize similar technology, the use case will be adjusted to support multiple documents and streamline generation of documentation.

The core idea is to use a flavor of Markdown to support document generation and a Table of Contents (ToC) file to control the structure and content of the resulting document (or documents...1 ToC per document).  The ToC file essentially contains metadata and an entry for each section of the document.  Each entry specified the section number, the section title, and the path to the markdown defining that section content.  An automated builder will read this ToC file, assemble the specified content, and generate well formatted output using 1 or more templates.  Although just a concept at this time, the template is important because it allows the same content to be published in a format suitable for various audences or purposes.  For example, internally I may want to publish a well formatted web page (or site) for my teams, but I may have to publish the same content in a MS Word or PDF format for a customer deliverable.

Automated generation of content will remain a focus of this approach.  All too often I hear talented professionals tell me they must spend their time grinding through tedious activities to produce documents for weeks or even months on end.  This is not rewarding or sustainable for talented engineers.  Wherever feasible I will explore content generation and the integration of that into the flow.  The intent is to be somewhat opinionated, but not overly prescriptive.  For example, I may choose to strongly prefer and encourable scaled vector graphics formatting of images to promote better CM but will not preclude JPG or other binary image formats.  Alternatively, I may choose a particular text-based modeling solution for demonstrating capability but do not intend to exclude incorporation of alternatives in the future.

Another interesting consideration is that we often have requirements for our documentation.  Sometimes we must follow a DID, or we have page limits, or perhaps we have formatting constraints.  Ideally I'd like to be able to test such requirements using a test specification and automated acceptance test.

In the end, this is an experiment and a project intended to both entertain myself and enable a bit of personal professional development over a holiday break during a global COVID-19 pandemic.  I hope it results in something useful for the community.  If it goes well, I may present it at a future [DevOps for Defense meetup](https://devopsfordefense.org).

In order to explore the viability of this solution, I'll attempt to create something that supports document generation of itself...employing the concept of "dog fooding".  

## Initial Design Thoughts
I'm a big fan of Gradle and Java.  It's what I know best so that's where I'm going to start.  Although I thought it might be nice to create a Gradle plugin, initially I'll just create an application that can be run from the command line.  I initialized the repo as an application and library using gradle init with the idea that I may want to reuse the library later for a gradle plugin project.

I'm going to use an MVP approach.  Since I don't know how things will go I'm just going to start small with an initial hypothesis:  If I concatenate multiple markdown files into a single set of content I can successfully generate HTML documentation.  My gut tells me this is super easy...but we'll see.

### Useful stuff (maybe)
Just want to keep track of a few items here that may be useful as I get started.
1. HTML Parser for testing output:  https://github.com/jhy/jsoup
1. Markdown Perser/Generator:  https://github.com/vsch/flexmark-java
