# On Post Word With String Hook

<!-- TOC -->

- [Use Post Word With String Hook](#use-post-word-with-string-hook)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the usePostWordWithStingHook.


```plantuml

@startuml

title usePostWordWithStringHook()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook: usePostWordWithString" as hook
  participant "Lambda" as lambda
  participant "Hook: usePostWord" as usePostWord
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
	user -> fe: User enters some words
	activate fe
		user <- fe: Shows the entered words
	deactivate fe
	user -> fe: Enters the word to posted
	activate fe
		fe -> hook: onClickPostWord()
		activate hook
			hook -> lambda: Ask lambda to parse the given string into object
			activate lambda
				hook <- lambda: Returns the perse object
			deactivate lambda
			hook -> usePostWord: Ask usePostWord to post the word
			activate usePostWord
				usePostWord -> api: postWordApi()
				activate api
					usePostWord <- api: Return the posted word
			  deactivate api
				usePostWord -> recoil: set(wordIdsState,[postedWord.id,...wordIds])
				usePostWord -> recoil: set(wordsFamily(postedWord.id),postedWord)
				usePostWord -> recoil: set(semestersState,semesters.semesters)
				hook <- usePostWord: Returns nothing
			deactivate usePostWord
			fe <- hook: Returns nothing
		deactivate hook
		user <- fe: Returns nothing
	deactivate fe
deactivate user
```