```plantuml

@startuml

title onClickPostWordFromUndo()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook" as hook
  participant "IsLoading" as useState
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box


activate user
  user -> fe: Click undo button
  activate fe
    fe -> hook: usePostWordFromUndo()
    activate hook
      hook -> useState: setLoading(true)
      activate useState
        useState -> useState: Sets isLoading to true
        hook <- useState: Done
      deactivate useState
      hook -> recoil: getPromise(wordsFamily(undoingWordId))
      activate recoil
        hook <- recoil: Return word data
      deactivate recoil
      break if word data is undefined
       user <- hook: show nothing / failed to re-post word
       end break
      hook -> api: postWordApi(word)
      activate api
        hook <- api: return posted (created) word
      deactivate api
      hook -> recoil: getPromise(wordIdsState)
      activate recoil
        hook <- recoil: wordIdsState
      deactivate recoil
       hook -> hook: id -> postedWord.id //if wordId === undoing wordId
      hook -> hook: id //If the above conditions are not met, the value is retained as is
        hook -> recoil: set(wordIdsState, wordIds)
        hook -> recoil: set(wordsFamily(postedWord.id), postedWord)
        hook -> recoil: set(semestersState, semesters.semesters)
      deactivate recoil
      fe -> user: show wordcards
      activate useState
        useState -> useState: Sets isLoading to false
        hook <- useState: Done
      deactivate useState
      fe <- hook: Returns undefined
    user <- fe: Returns nothing
    fe <- hook: usePostWordFromUndo
    hook -> useState: setLoading(false)
    deactivate hook
  deactivate fe
deactivate user