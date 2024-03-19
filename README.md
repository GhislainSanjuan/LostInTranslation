# Lost in translation : How to break the language barrier in Appsheet

The context
----

When you work with several teams across the globe, language barrier can be a problem. 

Let’s say, you have an Appsheet wiki with informations about safety procedures. 

But teams in other countries want to be able to display the fields and its content in their own language…

So how to do this ? 
----





## 2 solutions
1.Create a Google Chrome extension translating the data
- Needs strong coding skills
- Needs to be tested with different environments (with or without VPN,security features,...)
> A complex solution

2.Adapt your Appsheet application to translate content
- No coding skills needed except literally 3 line of Apps Script 
- Stay in the Appsheet environment
> A much more affordable solution

Let’s see how to create the solution N°2 with the following links : 
- if you want to copy the application  : [Lost in translation](https://www.appsheet.com//templates/How-to-break-the-language-barrier-in-Appsheet?appGuidString=b1a21096-36d5-44c1-9350-640b34b95a28).
  > Don't forget the Apps Script code :
  ```javascript
  function setTranslationForEntriesToTranslate() {
  let SP_TRANSLATIONS=SpreadsheetApp.openById("18hdWPb1Z5yP0UqUzv3cPEu6e0g4glI3r9678YyUy9Hs").getSheetByName("TRANSLATIONS")
  let translationDATA=SP_TRANSLATIONS.getDataRange().getValues()
  let entriesToTranslate = translationDATA.filter(x=>x[7]==true)
  entriesToTranslate.forEach(function (x) {
    let content = x[2] == "null" || x[2]=="" ? x[4] : x[5]
    let translationEntry = LanguageApp.translate(content, "", x[3])
    Logger.log(translationDATA.map(t=>t[1]).indexOf(x[1])+2)
    SP_TRANSLATIONS.getRange(translationDATA.map(t=>t[1]).indexOf(x[1])+1,7,1,2).setValues([[translationEntry,false]])
    Utilities.sleep(10)
    })
   }
  ```
- If you want the explanations in Google Slides : [Slides Lost in translation](https://docs.google.com/presentation/d/1fBpucLWDtZVLkxB4z7XZk9h5-3jAmRlEvEZ-TgAYWF8/edit#slide=id.g2aadba26b00_0_32).



## Improvements

In the template application, some behaviours have been defined in a certain way, but you can change them : 
- When a field is updated, no automation is launch but you can create this case using the same method as the update safety card.
- The translations could be created  on demand with a button and not automatically
- If you want to translate another table,you'll need to recreate some automation and change the table name in the formula. Maybe there is a way to automate this with a TABLES_MAP king of table




