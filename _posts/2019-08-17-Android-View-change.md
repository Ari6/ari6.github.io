---
layout: post
comments: true
categories: [Java, kotlin, Android, JavaFX]
---

# Android app development

This is whole another story from JavaFX development. I got stuck at beggining.

You can learn basics from [Android Developer site].(https://developer.android.com/guide/) In my opinion, this is not the greatest but there are lots of important and good information. If you need more code samples, you need to look up online.
You can also use kotlin but the way how to use APIs is almost the same. 

I needed to understand their language first. I meant words that they use.

## Glossary
* ViewGroup objects
	* A hierarchy of layouts(and containers)
	* ViewGroup can have children views(components).
	* Such as
		* LinearLayout
		* GridLayout
		* AdapterView
* View objects
	* a.k.a widgets
	* Such as 
		* TextView
		* ImageView
* Constraints
	* You need to set constraints among each objects.
	* This is really important that set components on a layout.
* Activities and Fragments
	* Presentation layer
* ViewModel
	* Business Logic
* Repository
	* knows where the date is stored.
	* Room library - local
	* Retrofit library - web

## layout
These are view xml files.

## Strings.xml
This is constant words list. When you want to show something on the button or other View objects, you should use this.

## manifests
You need to descrie essential information about the app. Such as activity, service information.

## Summary
* The words that they use is different but basics of GUI application is the same.
* Setting up calling method for action is almost the same as JavaFX.
* Data sharing with the other view is simpler but there are some ways to do.
* ListView handling is different.

categories: [Java, kotlin, Android, JavaFX]