# qualtrics-tlx
Custom css for NASA-TLX in Qualtrics

## Summary 

The NASA-TLX (Task Load Index) is the gold standard subjective (self-report) measure of workload. By default, it is administered as a paper-and-pencil questionnaire. Many researchers have administered it digitally using custom-built survey tools, but this doesn’t work well when you need to include the TLX as part of a larger survey. Many papers also reference giving participants the TLX through Qualtrics, but there is a lack of documentation for how these digital versions are designed to mimic (i.e., look and act the same as) a hard copy of the scale. This document explains how to implement the Rating Sheet part of the TLX in Qualtrics. 

Description from NASA: https://humansystems.arc.nasa.gov/groups/tlx/index.php 

PDF of the paper-and-pencil version: https://humansystems.arc.nasa.gov/groups/tlx/downloads/TLXScale.pdf 

### Set up a TLX Qustion in Qualtrics

In your Qualtrics survey, create a “Qualtrics-ified” version of the TLX -- that is, make as close an approximation of it as possible with Qualtrics’ built-in question types.

How to do this: 
Create a Slider question.
Give it 6 statements.
Give it a custom start position for the handle in the middle of the scale.
Toggle the “Custom start position” feature in the sidebar ON.
Toggle “Grid lines” ON. They will make sure your custom start positions stay where you want them to.
Give it 3 grid lines, and check the “Snap to grid” box.
Drag each handle to the middle of its slider. It should snap to the middle grid line.
Toggle “Grid lines” OFF. You don’t want them there for the actual survey. 
Whatever position you leave each handle in will be its custom start position. Assuming you didn’t move them after positioning them in the middle of the slider, they should stay in the middle. 
Don’t Add labels or Show value.
Add the Question text.
You can use “Please use the sliders to answer each question below”, but this isn’t official or validated -- edit it as you see fit.
Add the Statement text.
Mental Demand: How mentally demanding was the task?
Physical Demand: How physically demanding was the task?
Temporal Demand: How hurried or rushed was the pace of the task?
Performance: How successful were you in accomplishing what you were asked to do?
Effort: How hard did you have to work to accomplish your level of performance?
Frustration: How insecure, discouraged, irritated, stressed, and annoyed were you?
At this point, your complete survey question should look like this: 

And, if you preview it (three dots at the top right of the question box -> Preview question): 


### Target your TLX question with JavaScript.

Open your TLX question’s JavaScript window.
With the question selected, scroll down on the left sidebar until you see “</> Javascript”, and open that. 
There will probably be some Qualtrics template JS already there. The function you want to edit is the first one, Qualtrics.SurveyEngine.addOnload().
Turn the onLoad() function into the following by copy-pasting the code between the brackets into what’s already there: 
Qualtrics.SurveyEngine.addOnload(function()
{
	/*Place your JavaScript here to run when the page loads*/
	var qid = this.questionId;	
	jQuery('#' + qid).attr("id", "nasa-tlx");

});
This finds the html element that is your question and changes its id to nasa-tlx. This is necessary because Qualtrics changes question IDs as you add new questions, Auto-number, etc. By always assigning this question the same ID when it loads, you have a reliable identifier for it. 
Make sure you don’t somehow give any other questions an id of nasa-tlx to any other element in your survey. (Not that there’d be any reason at all to do that. :P) 

### Apply Custom CSS to turn the sliders into graded scales.

Copy the raw content of the tlx.css file in this repo.
Go to the Style tab of your survey’s Look and Feel, and paste the css you copied into the Custom CSS box.

