---
published: false                        
type: workshop                          
title: Continuous Integration Pipeline
short_title: Continuous Integration Pipeline    
description: In this workshop, you’ll create a continuous integration pipeline for your tests. Continuous Integration (CI) automates the testing of code whenever the code changes. This ensures code quality remains high and encourages regular merging and testing. You’ll use Azure DevOps to create and run a CI pipeline to build code, then run XUnit-based tests, set up filters for different tests, and add code coverage for analysis of run results.                   
authors:                                    
  - Name
contacts:                               
  - Author's email,
duration_minutes: 60                    
tags: ci, pipeline, Azure DevOps          
#banner_url: assets/banner.jpg           # Optional. Should be a 1280x640px image
audience: devs, devops
#wt_id: <cxa_tracking_id>                # Optional. Set advocacy tracking code for supported links
#oc_id: <marketing_tracking_id>          # Optional. Set marketing tracking code for supported links

---

# Introduction

## 1.1 About the workshop
You are an experienced C# developer, and you just arrived to your new job at eStore Connect, a company specializing in e-commerce solutions.

You have been developing C# code for some time and have tried writing unit tests, but you never got around to fully using automated tests as part of your development job. Your new company uses the latest and greatest technologies, and you were told in your interview that they practice many Agile methodologies and rely heavily on automated tests, from unit tests to acceptance tests, to make sure that new code works as requested and enables fast development cycles.

Today, you were given an interesting task. Create a continuous integration pipeline for the code and tests that you were working on for your code. Although you have never tried configuring a build server, you are sure you can handle this assignment using your software development skills and a bit of documentation reading.

Continuous integration (CI) is the process of automating the building and testing of code whenever the code changes. This practice ensures that the code quality remains high, encourages developers to merge their code, and tests several times per day. Every commit (or push) to the main branch triggers a process that builds, runs all the tests, and reports the results of that build. Build results can then be aggregated to provide insight into the health and quality of the codebase, and if a bug is accidentally introduced to the main codebase, then it is caught and handled immediately.

In this workshop, you will create a continuous integration (CI) pipeline using Azure DevOps. It will build your code and run your unit and integration tests that were created in the previous projects. After you have the proper build process in place, you can continue using it as you add more functionality and tests in the upcoming projects.

## 1.2 Techniques employed

In this project, you will learn how to set up a build server that will help you guarantee the quality of your code. Among other things, you will learn the following:

  * How to set up a CI server that automatically runs all of your tests when your code changes
  * How to decide what tests to run on each pipeline
  * How to collect and analyze data from your continuous integration run

## 1.3 Project Outline

This workshop will be broken into three milestones.

1. Create a New CI Pipeline to Build and Test Your Code

    * We will start from the result of the previous project; that project has a decent number of unit tests as well as integration tests. We will sign up and register for a free Azure DevOps account. Then we will connect the account to our repository and build a minimal CI pipeline that will build our code and run all of the xUnit-based tests in our project.
    * The solution is the pipeline definition exported from Azure DevOps site.

2. Use Filters to Decide What to Test

    * Once we have a pipeline that runs unit and integration tests, we can choose not to run all tests during our CI build. We will use filters in our build configuration and our code to decide which tests to run in our build and which to ignore.
    * The solution is the pipeline definition exported from Azure DevOps site.

3. Add Code Coverage

    * Once we have the proper build pipeline, we can set up triggers and add code coverage to our test run, and then we will use the built-in analytics and the website to view statistics and analyze the run results.
    * The solution is the pipeline definition exported from Azure DevOps site.

## 1.4 Prerequisites

This workshop is for intermediate C# developers / DevOps who want to know how to use a build server and create continuous integration as part of their automated testing strategy.

A big part of this project will use existing code, so you should be able to to read, compile, and run C# code using Visual Studio.

TOOLS
  - YAML: You should be able to read simple YAML files, but if you have never seen a YAML file before, don’t worry; it will be simple, per our needs.
  
  - Visual Studio: You should have work experience with Visual Studio and be able to create new projects and install plugins. When installing Visual Studio, be sure to install the following workloads.
  
  - ASP.NET and web development
  
  - .NET desktop development
  
  - .NET Core cross-platform development
    It is also possible to use Visual Studio Code instead as long as you have prior experience with developing .NET Core applications using VS Code.
  
  - MongoDB: You should have basic familiarity as this will be used as the DB of the project.
  
  - Docker: You should have a basic level of understanding; you will need to be able to run Docker and Docker Compose files from Visual Studio. We will also use Docker to run needed dependencies in the tests.

Enthusiasm for solving problems and self-led learning will also prove quite useful (and not just in this project)!

## 1.5 Libraries & Tools

Our main development will be done using Visual Studio 2022. If you do not have Visual Studio (VS) installed, you can download and install the freely available Community edition from [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/).

It is also possible to use VS Code instead as long as you are familiar with it and can run and debug the tests and code supplied with this project.

In order to run the different projects, you will need to have Docker installed as well; installation depends on your OS of choice. I highly recommend downloading and installing Docker Desktop, which is found at [Docker Desktop overview](https://docs.docker.com/desktop/).

The starting project will be either the result of the previous project or the project folder

## 1.6 Technology versions

| Technology | Minimum Version Required | Max Supported (Current) Version | 
|----------------|-----------------|-----------------|
| .NET                  | 5.0           | 7.0         |
| Visual Studio         | 2019          | 2022        |
| Docker Desktop        | -             | -           |
| Azure DevOps Pipeline | -             | -           |  

## 1.7 Upgrading projects to use .NET 6.0 or 7.0

.Net 6 is an LTS (Long Term Support) version of the .Net framework. .Net 6 will be supported by Microsoft for three years from its release. The previous version, .Net 5, is officially out of support from Microsoft but it can still be used for local projects for learning. You can upgrade the solutions in this liveProject from .Net 5.0 to .NET 6.0 (LTS) or .NET 7.0 (Current), by carrying out the following steps. You can substitute 7.0 for 6.0 throughout if you prefer the current version of the .NET framework.

  1. Upgrade the Target Framework
  * Open the solution in Visual Studio, right-click on the project file and select ‘Properties’ from the bottom of the context menu. Change the target framework to .NET 6.0 and save the project.
  * Alternatively you can edit the project’s .csproj file directly and change the target Framework from net5.0 to net6.0.

  2. Update the Docker Image
  * Open the file <code>Dockerfile</code>.
  * Change the base image from <code>mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim</code> to <code>mcr.microsoft.com/dotnet/aspnet:6.0-bullseye-slim</code>.

You should now be able to run the project under .Net 6.0

<i>Optional</i>

Delete obj and bin folders to clean up old .Net 5.0 files

If you have any issues with the project not building or running, you may need to delete the existing bin and obj folders. You may also do this if you want to remove out-of-date files from your project. Go to the respective project directory and delete the ‘bin’ and ‘obj’ folders.

Additionally, you can delete the NuGet cache by running this command:

<code>dotnet nuget locals --clear all</code>

When you build the project the folders will be recreated and the project will be built using the new .Net 6.0 files.

## 1.7 Recommended resources

These resources, identified by the author, can directly impact or expand your understanding of the liveProject’s content. These resources do not need to be read in advance of starting the project.

Please note: You will have full access to these Manning materials for the first 90 days after starting the project in addition to the excerpts within the project. After 90 days, you will still have access to the excerpts, and you will only be able to see a preview of the resources if viewed outside the project.

  * <p><i>The Art of Unit Testing, Second Edition </i> by Roy Osherove</p>

  * <p><i>Unit Testing Principles, Practices, and Patterns </i> by Vladimir Khorikov</p>

  * <p>Azure DevOps documentation</p>

  * <p>Getting Test Results in Azure DevOps Pipelines</p>

We provide additional resources and tutorials throughout the project. Feel free to use any resources you can find to complete the workshop.

## 1.8 Further reading

These are additional resources that may be helpful to further your understanding of the workshop's content.

 - [Continuous Integration in .NET](https://livebook.manning.com/book/continuous-integration-in-dot-net/about-this-book/) by Marcin Kawalerowicz and Craig Berntson: Use this to understand the motivation and flow of CI builds; skip the chapters about different .NET build servers as it is out of date.

---

# Create a CI Pipeline to Build and Test Your Code

## 2.1 Objective

Create a CI pipeline that will compile and run all of the tests for your project on each commit.

## 2.2 Importance to project

Running your automated tests when code changes will provide quick feedback and help you catch bugs as they are introduced into the system. Although you should run all your tests before committing your code, sometimes you will forget to run some of the tests or an issue will be introduced due to merging with code from other members of your development team. By running your tests continuously, you will also make sure that they keep working and avoid “test rot.” And finally, you will be able to rapidly change your code, knowing that your build server keeps your code and tests running according to requirements.

## 2.3 Workflow

We will start with the result of the previous workshop, which you can download below. That workshop has a decent number of unit tests as well as integration tests. We will sign up and register for a free Azure DevOps account. Then we will connect the account to our repository and build a minimal CI pipeline that will build our code. We will run all of the xUnit-based tests in our project. We will then use tags and/or test names to filter our pipeline so that it will only run unit tests that do not require any external dependencies.

If you have not done so already, download the previous workshop from this [repository](assets/start_solution.zip).

1. Sign up for a [free Azure DevOps account](https://azure.microsoft.com/en-us/products/devops/).

2. Create a new project and a new pipeline.
   
    * <p>Once you log in to your Azure DevOps account, create a new project.</p>
    * <p>If you did not complete the previous project in the series or do not want to use your code, you can use the start solution.</p>
    * <p>If your project is not hosted on a source control server, you can import it now using the Repo tab.</p>
    * <p>Go to the pipeline, choose a new pipeline, and link it to the repository where the code from the previous project resides.
    * Configure your pipeline; you will need to choose ASP.NET Core.
      * <p>If you have uploaded the code using Repo, you can create the build from the Repo tab.</p>
    * Read the resulting YAML, make sure you understand what it does and that it’s correct, then save and run your new pipeline.
      * <p>Alternatively, you can start from scratch and create the needed steps based on Azure DevOps documentation.</p>
    * Make sure the build runs and finishes successfully.

<div class="tip" data-title="Tip">

> * When the build is running, you can click on Job to see the build output as it runs.
> * You can change your build script any time by selecting "Edit Pipeline"; it’s next to the blue “run” button.

</div>

3. Update your pipeline definition so that all of the tests will run.

  * <p>Once the build has finished, go to the specific run and verify that the tests have run using the “tests” tab</p>

<div class="tip" data-title="Tip">

> Feel free to experiment; there are at least two ways to run .NET Core tasks in Azure DevOps.

</div>

<details>
<summary>Resource Tip</summary>
<div class="tip" data-title="Tip">

Feeling stuck? Use as little or as much help as you need to reach the solution! 

  * [Microsoft-hosted agents](https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/hosted?view=azure-devops&tabs=yaml) is a list of available VMs to run your build on.
  * [Azure DevOps documentation](https://learn.microsoft.com/en-us/azure/devops/?view=azure-devops)
  * [Getting Test Results in Azure DevOps Pipelines](https://xunit.net/docs/getting-test-results-in-azure-devops)
  * Setup .NET Core using [.NET Core task](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/reference/use-dotnet-v2?view=azure-pipelines&viewFallbackFrom=azure-devops)
  * Execute .NET Core command using [.NET Core CLI task](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/reference/dotnet-core-cli-v2?view=azure-pipelines&viewFallbackFrom=azure-devops)

</div>
</details>

<details>
<summary>Partial Solution</summary>
  
  Feeling stuck? Use as little or as much help as you need to reach the solution!
  Here is the partial solution for this milestone. Use it to develop your own full solution.
  
  [Download Partial Solution](assets/M1_solution_partial.yml)

</div>
</details>

<details>
<summary>Full Solution</summary>
  
  If you are unable to complete the project, you can download the full solution here. We hope that before you do this you try your best to complete the project on your own.
  
  [Download Full Solution](assets/M1_solution_full.yml)

</div>
</details>

---

# Use Filters to Decide What to Test

## 3.1 Objective

Learn how you can affect what tests will run based on the test names and test metadata.

## 3.2 Importance to project

 * Currently, we need to run all of our tests, but as your test suite grows and a higher level of tests (acceptance, E2E) are added to your project, you will find that you do want to run all of the tests all of the time. Maybe you want your long-running tests to run only on a nightly build, or maybe you have a few tests you can only run on your machine. In the future, you will be able to split the tests into fast-running CI tests, long-running nightly builds, and/or system-wide sanity tests depending on your needs.

## 3.3 Workflow

1. Run one unit test using the test name.
    * <p>Currently, the tests run pretty fast (~35 seconds), but usually, we like to choose which tests to run, avoid long-running tests and tests that require complex setup, and only run our unit tests.</p>
    * <p>Make the change and verify this time only that the unit test has run.</p>

3. Run tests based on categories.
    * <p>Another way to filter and mark tests is based on categories, which in xUnit are called Traits.</p>
    * <p>Use Traits to mark unit tests as “Unit” tests and all integration tests as “Integration” tests.</p>

    <div class="tip" data-title="Tip">

    > You can check your traits in the Test Explorer window in Visual Studio and make sure you have not forgotten any test.

    </div>

    * <p>Change the build script to run only integration tests based on categories.</p>
    * <p>After the CI build finishes, check the tests tab; you should see 11 tests that run.</p>

3. Set the assembly-level trait.

    * <p>Mark all currently available tests as “Build” and "CI"; use the special assembly trait to mark all of the tests in the test assembly.</p>
    * <p>Update the build script to run all tests that are marked as CI.</p>

    <div class="info" data-title="Note">

    > Do not forget to push your changes to your source control before running the build.

    </div>

    <div class="tip" data-title="Tip">

    > Using filtering is a powerful capability, but it also one that can cause a lot of issues if not handled correctly. If, for example, you have set the build to only run a specific set of tests based on their name, and you write new tests that do not use the same naming convention, you might end up with some of you tests not running on each commit. The ideal solution is to always run all of your tests and only filter out tests you explicitly decide not to run.

    </div>

<details>
<summary>Resource Tip</summary>
<div class="tip" data-title="Tip">

> [Run selective unit tests](https://learn.microsoft.com/en-us/dotnet/core/testing/selective-unit-tests?pivots=xunit)

</div>
</details>

<details>
<summary>Workflow Tip</summary>
<div class="tip" data-title="Tip">

> <p>Step 1 Hint</p>
> <p>Running based on test class is not possible with xUnit; instead, you need to define a specific string in the displayed test name.</p>

> <p>Step 3 Hint</p>
> <p>Use xUnit’s <code>AssemblyTraitAttribute</code> to set assembly-wide categories (traits); just add the following line in one of the test classes files (e.g., *TestBase.cs): [assembly: AssemblyTrait("Build", “CI”)].</p>

</div>
</details>


<details>
<summary>Partial Solution</summary>
  
  Feeling stuck? Use as little or as much help as you need to reach the solution!
  Here is the partial solution for this milestone. Use it to develop your own full solution.
  
  [Download Partial Solution](assets/M2_solution_partial.yml)

</div>
</details>

<details>
<summary>Full Solution</summary>
  
  If you are unable to complete the project, you can download the full solution here. We hope that before you do this you try your best to complete the project on your own.
  
  * [Download YAML Solution](assets/M2_solution_full.yml)
  * [Download Full Solution](assets/M1_solution_full.zip)

</div>
</details>

---

# Adding Code Coverage

## 3.1 Objective

Now that we have a proper build pipeline, we can set up triggers and add code coverage to your test run. Then we will use the built-in analytics and the website to view statistics and analyze the run results.

## 3.2 Importance to project

* Using code coverage, we will be able to discover if we have forgotten to test a scenario and better understand the quality of our testing efforts. Having code coverage as part of the CI build will enable us to compare test runs and check if the quality of our projects increases by investigating the code coverage trend.

## 3.3 Workflow

1. Make sure you have coverlet.collector in your test project dependencies.
    * <p>If you have created a project of the xUnit type, all you need to do is make sure it is the latest version.</p>

2. Add code coverage analysis to test run.
    * In the test run, steps add the needed parameter to run the coverlet.
        * [See Publish Code Coverage Results task](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/test/publish-code-coverage-results?view=azure-devops).
    * <p>Add a task to publish code coverage results.</p>
    * <p>Check that code coverage details appear both in the <i>summary</i> tab and under a new <i>code coverage</i> tab.</p>

4. Add final touches, and you are done.
    * <p>Change the build trigger so the build will be executed when code has been updated in any branch of your source control, not just the main one.</p>
    * <p>Add display names to the different tasks of your project.</p>
    * Browse the [Visual Studio Marketplace](https://marketplace.visualstudio.com/azuredevops/) for new tasks to install in your “organization.” You do not need to install any extension, but if you see one that could benefit you, install it and configure it for your build.
    * Connect your Visual Studio to your project, view test results, and trigger builds from within Visual Studio.
      * [Navigate in Visual Studio Team Explorer](https://learn.microsoft.com/en-us/azure/devops/user-guide/work-team-explorer?view=azure-devops).<br>
    * In your project, create a new dashboard to show test results.
      * [Add, rename, and delete dashboards in Azure DevOps.](https://learn.microsoft.com/en-us/azure/devops/report/dashboards/dashboards?view=azure-devops)

<div class="info" data-title="Note">

> Investigating failures on build servers can be difficult, especially when adding new capabilities. Start by reading the run logs and checking the locations of all created files, making sure that the files were created where you expect them to exist. And if all else fails, try to run the same command on your dev machine, and see if you have any errors.

</div>


<details>
<summary>Resource Tip</summary>
<div class="tip" data-title="Tip">

> * [Coverlet on GitHub](https://github.com/coverlet-coverage/coverlet)
> * [Publish Code Coverage Results task](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/reference/publish-code-coverage-results-v1?view=azure-pipelines&viewFallbackFrom=azure-devops)

</div>
</details>

<details>
<summary>Workflow Tip</summary>
<div class="tip" data-title="Tip">

> <p>Step 2 Hint</p>
> * If you have issues finding the coverage result file, make sure it has been created then use either (Agent.TempDirectory)(Agent.TempDirectory) or (Build.SourcesDirectory)(Build.SourcesDirectory) to look in the right location.

> Step 3 Hint
> * [Azure DevOps CI triggers GitHub](https://learn.microsoft.com/en-us/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml#ci-triggers)

</div>
</details>

<details>
<summary>Full Solution</summary>
  
  If you are unable to complete the project, you can download the full solution here. We hope that before you do this you try your best to complete the project on your own.
  
  * [Download Full Solution](assets/M3_solution_full.yml)

</div>
</details>

---

## Summary

  * <p>Using a CI pipeline, we can automatically build and test our code and provide insights into the code quality.</p>
