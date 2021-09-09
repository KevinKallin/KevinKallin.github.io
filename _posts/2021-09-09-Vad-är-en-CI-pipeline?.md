---
layout: post
title: "Vad är en CI pipeline?"
date: 2021-09-09 09:23:00
tags: CI/CD ContinousIntegration ContinousDeployment Workflow
--- 

### Vad är en CI/CD pipeline?

En CI/CD pipeline är ett sätt för att utveckla applikationer. Det körs i flera olika steg för att leverera nya versioner av en mjukvara. 
CI/CD pipelines är en fokuserad tillämpning av att förbättra mjukvaruleveranser när man använder sig utav antingen en 
[DevOps](https://www.redhat.com/en/about/videos/learn-cloud-native-series-what-is-devops) eller [SRE](https://www.redhat.com/en/topics/devops/what-is-sre) metod. 

CI introducerar övervakning och automatiseringen för att förbättra processerna av apputveckling, framförallt för testningsfaserna och integrationen
men också under leverans och mjukvaruimplementeringen(deployment)

### Stegen för en CI/CD pipeline
  
  * Build - Utvecklarna kompilerar koden från applikationen
  * Test - <em>The quality assurance(QA)</em> teamet testar koden för applikationen och använders sig av automatiserade testverktyg och strategier. 
  * Release - I denna fas sker leveransen av applikationen till repository
  * Deploy - Fasen som koden blir utplacerad till produktion
  * Validation och Compliance - I denna fasen validerar man en build ifall den är det behovet som din organisation behöver / kräver.


### Implementering av CI/CD i eget projekt

Jag och Mikael implementerade CI/CD utifrån hans projektgrupp med SpacePark version 1. 

Vi gjorde det i följande steg:

  * "Forkade" projektet till eget repository
  * Fixade ett workflow, genom att skapa ny mapp som heter .gitub/workflows. Inuti den mappen skapade vi en fil som heter action.yml.
  * Inuti action-filen så började vi med att lägga till att en action sker efter varje commit (on: push)
  * Skapade upp en build som sedan körs på senaste ubuntu versionen.
  * Ställde in vilken version av dotnet som ska köras, blev 5.0, då det är den versionen som projektet kördes på. 
  * Sist ställde vi för att kunna köra två olika actions på samma fil (SpacePark/sln). 


### Beskrivning av vårt workflow

![image](https://user-images.githubusercontent.com/65369996/132680438-3ab07efd-579c-425c-b389-d4b89eb5924d.png)

*Texten efter hashtaggen i bilden beskriver varje rad* 

### Referenser 

[What is a CI/CD pipeline?](https://www.redhat.com/en/topics/devops/what-cicd-pipeline)

[OpenSource CI/CD](https://opensource.com/article/21/6/what-cicd-pipeline)






