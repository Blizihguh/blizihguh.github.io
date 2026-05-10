---
layout: page
title: Progress Update Generator
permalink: /code/progress-update-generator/
description: Progress update generator
---

<!-- HTML -->
<b>Update Template</b><br />
<label><input type="radio" onchange="update_preview('two_month_update')"         name="progress_update_type" >Two Month Update | </label>
<label><input type="radio" onchange="update_preview('first_practice_test')"      name="progress_update_type" >First Practice Test | </label>
<label><input type="radio" onchange="update_preview('official_test_upcoming')"   name="progress_update_type" >Official Test Upcoming | </label>
<label><input type="radio" onchange="update_preview('major_milestone_achieved')" name="progress_update_type" >Major Milestone Achieved </label><br />
<label><input type="radio" onchange="update_preview('student_missing_class')"    name="progress_update_type" >Student Missing Class | </label>
<label><input type="radio" onchange="update_preview('student_unprepared')"       name="progress_update_type" >Student Unprepared | </label>
<label><input type="radio" onchange="update_preview('scores_not_increasing')"    name="progress_update_type" >Scores Not Increasing |</label>
<label><input type="radio" onchange="update_preview('start_of_academic_year')"    name="progress_update_type" >Start of Year </label>

<b>Purchase Link</b><br />
<label><input type="radio" onchange="update_purchase('academics_pt')" name="purchase_type" >Academics/Private Tutoring |</label>
<label><input type="radio" onchange="update_purchase('back_up_care')" name="purchase_type" >Back-Up Care |</label>
<label><input type="radio" onchange="update_purchase('none')"         name="purchase_type" >None</label>

<div id="textboxes" style="width:50%; float:left;">
	Student is... 
	<label><input type="radio" onchange="update_gender('male')" name="gender_select">Male</label>
	<label><input type="radio" onchange="update_gender('female')" name="gender_select">Female</label>
	<label><input type="radio" onchange="update_gender('other')" name="gender_select">Other</label><br />
	<label style=" display: inline-block; min-width: 170px">Parent Name:</label><input type="text" id="parent_name" oninput="populate_template('parent_name')"><br />
	<label style=" display: inline-block; min-width: 170px">Student Name:</label><input type="text" id="student_name" oninput="populate_template('student_name')"><br />
	<label style=" display: inline-block; min-width: 170px">Time Period:</label><input type="text" id="time_period" oninput="populate_template('time_period')"><br />
	<label style=" display: inline-block; min-width: 170px">Growth Areas (General):</label><input type="text" id="areas_of_improvement" oninput="populate_template('areas_of_improvement')"><br />
	<label style=" display: inline-block; min-width: 170px">Growth Area (Specific):</label><input type="text" id="area_of_progress" oninput="populate_template('area_of_progress')"><br />
	<label style=" display: inline-block; min-width: 170px">Objective Achieved:</label><input type="text" id="objective_achieved" oninput="populate_template('objective_achieved')"><br />
	<label style=" display: inline-block; min-width: 170px">Short-Term Goal:</label><input type="text" id="short_goal" oninput="populate_template('short_goal')"><br />
	<label style=" display: inline-block; min-width: 170px">Long-Term Goal:</label><input type="text" id="long_goal" oninput="populate_template('long_goal')"><br />
	<label style=" display: inline-block; min-width: 170px">Velocity Suggestion:</label><input type="text" id="velocity_suggestion" oninput="populate_template('velocity_suggestion')"><br />
	<label style=" display: inline-block; min-width: 170px">Velocity Date:</label><input type="text" id="velocity_date" oninput="populate_template('velocity_date')"><br />
	<label style=" display: inline-block; min-width: 170px" id="template_specific_1" >-</label><input type="text" id="template_specific_1" oninput="populate_template('template_specific_1')"><br />
	<label style=" display: inline-block; min-width: 170px" id="template_specific_2" >-</label><input type="text" id="template_specific_2" oninput="populate_template('template_specific_2')"><br />

</div>
<div id="preview" style="margin-left:55%">Select a template to see preview</div>

<script>
var CURRENT_TEXT = "";
var CURRENT_FORM = "";

var PARENT_NAME = "PARENT NAME";
var STUDENT_NAME = "STUDENT NAME";
var STUDENT_PRONOUN_HIS = "HIS/HER";
var STUDENT_PRONOUN_HE = "HE/SHE";
var STUDENT_PRONOUN_HIM = "HIM/HER";

var AREAS_OF_IMPROVEMENT = "AREAS OF IMPROVEMENT";
var AREA_OF_PROGRESS = "AREA OF PROGRESS";
var OBJECTIVE_ACHIEVED = "OBJECTIVE ACHIEVED";

var SHORT_TERM_GOAL = "SHORT TERM GOAL";
var LONG_TERM_GOAL = "LONG TERM GOAL";

var TIME_PERIOD = "TIME PERIOD";
var TEMPLATE_SPECIFIC_SECTION = "!!!!!!!";
var TEMPLATE_SPECIFIC_SECTION_2 = "#######";

var SUGGESTED_VELOCITY = "SUGGESTED VELOCITY"; // Include potential new subjects
var VELOCITY_DATE = "VELOCITY DATE";

var PURCHASE_INFO = "";

const APT_PURCHASE = "##### !!! REPLACE WITH MAGIC LINK !!! ###<br /><br />"
const BUC_PURCHASE = "If you'd like to continue working together on achieving these goals, you can redeem more credits through your Bright Horizons portal. After you redeem your credits, you will receive an email from Revolution Prep to add the hours to your account.<br /><br />";

function cap_first(val) {
	// Capitalize first letter of string
    return String(val).charAt(0).toUpperCase() + String(val).slice(1);
}

const TEMPLATES = {
	two_month_update: () => `Dear ${PARENT_NAME},<br/><br/>I hope you are having a great ${TIME_PERIOD}. It’s been great working with you and ${STUDENT_NAME} over the past couple of months! I wanted to touch base to share some of the progress we’ve made so far, and to share my thoughts on the plan moving forward.<br/><br/>I have seen significant improvements in ${STUDENT_NAME}'s ${AREAS_OF_IMPROVEMENT}. In particular, ${STUDENT_PRONOUN_HE} has shown consistent progress in ${AREA_OF_PROGRESS}. This has been reflected in ${OBJECTIVE_ACHIEVED}.<br/><br/>Our current short-term goals for ${STUDENT_NAME} include ${SHORT_TERM_GOAL}. The overall goal remains ${LONG_TERM_GOAL}. Based on ${STUDENT_NAME}'s progress, I recommend ${SUGGESTED_VELOCITY}.<br/><br/>${PURCHASE_INFO}Please let me know if you have any questions or if there are any adjustments you would like to make to our plan. I’m happy to schedule a time to talk by phone if that would be helpful. I look forward to supporting ${STUDENT_NAME} in ${STUDENT_PRONOUN_HIS} continued academic journey.<br/><br/>Best regards,`,
	first_practice_test: () => `Dear ${PARENT_NAME},<br /><br />I hope you are having a great week! As we prepare for ${STUDENT_NAME}'s upcoming practice test, I wanted to share some updates and information about what to expect.<br /><br />I have seen significant improvements in ${STUDENT_NAME}'s ${AREAS_OF_IMPROVEMENT}. ${cap_first(STUDENT_PRONOUN_HE)} has shown consistent progress in ${AREA_OF_PROGRESS}. This includes growth in areas we previously discussed as struggles, such as ${OBJECTIVE_ACHIEVED}.<br /><br />While we are working towards overall score improvement, we have also set a goal around successfully utilizing the strategies and skills they have been working on. It's important to remember that the score might go down on the next practice test, which is perfectly normal. Students often experience a drop in scores as they are learning to apply new strategies. This adjustment period can cause them to rush or not finish a section.<br /><br />To be set up for long-term success, it's crucial for ${STUDENT_NAME} to replicate official test day conditions as closely as possible when taking ${STUDENT_PRONOUN_HIS} practice test. ${cap_first(STUDENT_PRONOUN_HE)} should find a quiet place and take the test in one sitting.<br /><br />After the practice test, I will review the results and discuss the test experience with ${STUDENT_NAME} to determine our focus moving forward, and I’ll follow up with you on takeaways, improvements, and next steps in my next parent update.<br /><br />Based on our discussions and ${STUDENT_NAME}'s progress, I recommend ${SUGGESTED_VELOCITY}. I think this is a good plan going forward, and of course we will continue to monitor ${STUDENT_NAME}'s progress and potentially reevaluate ${VELOCITY_DATE}. This plan will best set ${STUDENT_NAME} up for success for ${STUDENT_PRONOUN_HIS} next official test.<br /><br />${PURCHASE_INFO}Please let me know if you have any questions or if there are any adjustments you would like to make to our plan. I’m happy to schedule a time to talk by phone if that would be helpful. I am excited to continue supporting ${STUDENT_NAME} in reaching ${STUDENT_PRONOUN_HIS} goals!<br /><br />Best regards,`,
	official_test_upcoming: () => `Dear ${PARENT_NAME},<br /><br />It’s been great working with you and ${STUDENT_NAME} over the past couple of weeks/months. As we prepare for ${STUDENT_NAME}'s upcoming test, I wanted to share some updates and information about what to expect.<br /><br />I have seen significant improvements in ${STUDENT_NAME}'s ${AREAS_OF_IMPROVEMENT}. ${cap_first(STUDENT_PRONOUN_HE)} has shown consistent progress in ${AREA_OF_PROGRESS}. This consistent improvement has been evident in ${OBJECTIVE_ACHIEVED}.<br /><br />For this exam, our goal is ${LONG_TERM_GOAL}. While we cannot guarantee a specific score, we have worked diligently towards this goal through ${SHORT_TERM_GOAL}. It's important to consider the impact of the test zone on ${STUDENT_NAME}'s performance. Ensuring a good night's sleep throughout the week leading up to the test is crucial! Just the night before isn't enough. We have also discussed strategies to manage test anxiety, which can impact scores.<br /><br />I am looking forward to hearing how ${STUDENT_NAME} performs on this test. Looking ahead, I recommend ${SUGGESTED_VELOCITY}. ${TEMPLATE_SPECIFIC_SECTION}.<br /><br />${PURCHASE_INFO}Please let me know if you have any questions or if there are any adjustments you would like to make to our plan. I’m also able to schedule a time to talk by phone if that would be helpful. I am happy to support ${STUDENT_NAME} in ${STUDENT_PRONOUN_HIS} continued academic journey.<br /><br />Best regards,`,
	student_missing_class: () => `Dear ${PARENT_NAME},<br /><br />I hope you are having a great day! I wanted to touch base regarding ${STUDENT_NAME}'s recent attendance and participation in our tutoring sessions.<br /><br />Firstly, I have seen significant improvements in ${STUDENT_NAME}'s ${AREAS_OF_IMPROVEMENT}. ${cap_first(STUDENT_PRONOUN_HE)} has shown consistent progress in ${AREA_OF_PROGRESS}, and this progress is commendable.<br /><br />However, I’ve noticed that there have been some inconsistencies in ${STUDENT_NAME}'s attendance. ${cap_first(STUDENT_PRONOUN_HE)} has frequently ${TEMPLATE_SPECIFIC_SECTION}, which can make it challenging to achieve the goals we’ve set. As a reminder, our goal is ${LONG_TERM_GOAL}, and maintaining a consistent schedule is crucial for ${STUDENT_NAME} to reach this goal.<br /><br />Moving forward, I suggest we revisit the current schedule to find days and times that might work better for ${STUDENT_NAME}. I recommend ${SUGGESTED_VELOCITY}. If adjusting the schedule isn't possible, increasing the time spent studying outside of session can help keep ${STUDENT_NAME} on track.<br /><br />${PURCHASE_INFO}Please let me know if you have any questions or if there are any adjustments you would like to make to our plan. I’m happy to schedule a time to talk by phone if that would be helpful. I am here to support ${STUDENT_NAME} and ensure ${STUDENT_PRONOUN_HE} has the best possible chance to succeed.<br /><br />Best regards,`,
	student_unprepared: () => `Dear ${PARENT_NAME},<br/><br/>I hope this email finds you well. I wanted to discuss ${STUDENT_NAME}’s preparation for our tutoring sessions and share some insights and our plan moving forward.<br/><br/>Firstly, I want to acknowledge that ${STUDENT_NAME} has shown great progress in ${AREAS_OF_IMPROVEMENT}. ${cap_first(STUDENT_NAME)} has consistently demonstrated improvement in ${AREA_OF_PROGRESS}, which I am really happy to see!<br/><br/>As you know, our goal is ${LONG_TERM_GOAL}. However, ${STUDENT_NAME}’s lack of preparation for our sessions is slowing progress towards these goals. It is crucial that ${STUDENT_PRONOUN_HE} comes to sessions prepared with the appropriate technology, completed assignments, and required materials, and to be free from distractions.<br/><br/>To address this, I would like to discuss our plan moving forward:<br/><br/>· Scheduling: If ${STUDENT_NAME} does not have enough time between school, sports, or other activities and our tutoring session, perhaps we can find another time that ensures there is enough time to prepare.<br/><br/>· Preparedness: It is important for ${STUDENT_NAME} to arrive on time, with all necessary materials (e.g., paper, pencil, completed assignments) ready, and to be free from distractions. This will maximize the effectiveness of our sessions.<br/><br/>· Session Efficiency: When ${STUDENT_NAME} spends the first several minutes of our session getting ready, it takes away valuable time that could be spent on learning content or strategies.<br/><br/>· Technology: It is imperative that ${STUDENT_NAME} has functional technology for ${STUDENT_PRONOUN_HIM} to get the most out of their tutoring sessions. It is necessary that ${STUDENT_PRONOUN_HE} has a laptop, desktop computer, or tablet with a working camera and keyboard ability, as well either sufficient power on their device or a nearby power cord to complete the class.<br/><br/>Based on ${STUDENT_NAME}’s needs, I recommend ${TEMPLATE_SPECIFIC_SECTION}. This adjustment will help by ensuring that ${STUDENT_NAME} is ready to start learning as soon as the session begins. As far as our schedule is concerned, I would recommend ${SUGGESTED_VELOCITY}.<br/><br/>${PURCHASE_INFO}Please feel free to reach out with any questions or concerns. I am happy to discuss further and adjust our approach as needed to support ${STUDENT_NAME}’s success. We can also schedule a time to talk by phone if that would be helpful.<br/><br/>Thank you for your continued partnership,`,
	scores_not_increasing: () => `Template ${CURRENT_FORM}`,
	major_milestone_achieved: () => `Template ${CURRENT_FORM}`,
	start_of_academic_year: () => `Dear ${PARENT_NAME},<br /><br />I know this time of year is busy, and I appreciate you taking the time to review this email. As we begin a new academic semester, I wanted to take a moment to share some updates about ${STUDENT_NAME}'s progress and outline our plans moving forward.<br /><br />Over the past ${TIME_PERIOD}, I have seen significant improvements in ${STUDENT_NAME}'s ${AREAS_OF_IMPROVEMENT}. In particular, ${STUDENT_PRONOUN_HE} has shown consistent progress in ${AREA_OF_PROGRESS}. This has been reflected in ${OBJECTIVE_ACHIEVED}.<br /><br />Our current short-term goals for ${STUDENT_NAME} include ${SHORT_TERM_GOAL}. The overall goal remains ${LONG_TERM_GOAL}. If there have been any changes or new goals for this semester, please let me know so we can adjust our plan accordingly.<br /><br />For this semester, our plan includes ${TEMPLATE_SPECIFIC_SECTION}. I would also like to check on ${STUDENT_NAME}'s availability to ensure our sessions fit into their current schedule. If there are any changes, please let me know so we can plan for sessions that align with your student’s schedule. You can also adjust the schedule from your student’s dashboard if that’s more convenient!<br /><br />Based on ${STUDENT_NAME}'s progress, I recommend ${SUGGESTED_VELOCITY}.<br /><br />${PURCHASE_INFO}Please let me know if you have any questions or if there are any adjustments you would like to make to our plan. I’m happy to schedule a time to talk by phone if that would be helpful. I am looking forward to continuing my work with ${STUDENT_NAME} and in these next steps of ${STUDENT_PRONOUN_HIS} academic journey.<br /><br />Best regards,`
};

function populate_template(updated_input) {
	switch (updated_input) {
		case 'parent_name':
			PARENT_NAME = document.getElementById("parent_name").value;
			break;
		case 'student_name':
			STUDENT_NAME = document.getElementById("student_name").value;
			break;
		case 'areas_of_improvement':
			AREAS_OF_IMPROVEMENT = document.getElementById("areas_of_improvement").value;
			break;
		case 'area_of_progress':
			AREA_OF_PROGRESS = document.getElementById("area_of_progress").value;
			break;
		case 'objective_achieved':
			OBJECTIVE_ACHIEVED = document.getElementById("objective_achieved").value;
			break;
		case 'short_goal':
			SHORT_TERM_GOAL = document.getElementById("short_goal").value;
			break;
		case 'long_goal':
			LONG_TERM_GOAL = document.getElementById("long_goal").value;
			break;
		case 'time_period':
			TIME_PERIOD = document.getElementById("time_period").value;
			break;
		case 'velocity_suggestion':
			SUGGESTED_VELOCITY = document.getElementById("velocity_suggestion").value;
			break;
		case 'velocity_date':
			VELOCITY_DATE = document.getElementById("velocity_date").value;
			break;
		case 'template_specific_1':
			TEMPLATE_SPECIFIC_SECTION = document.getElementById("template_specific_1").value;
			break;
		case 'template_specific_2':
			TEMPLATE_SPECIFIC_SECTION_2 = document.getElementById("template_specific_2").value;
			break;
	}

	update_preview(CURRENT_FORM);
}

function update_gender(gender) {
	if (gender == "male") { STUDENT_PRONOUN_HIS = "his"; STUDENT_PRONOUN_HE = "he"; STUDENT_PRONOUN_HIM = "him"; }
	else if (gender == "female") { STUDENT_PRONOUN_HIS = "her"; STUDENT_PRONOUN_HE = "she"; STUDENT_PRONOUN_HIM = "her"; }
	else {} // Other option currently unsupported. TODO
	
	update_preview(CURRENT_FORM);
}

function update_purchase(purchase_type) {
	// Call update_preview after
	if (purchase_type == "academics_pt") { PURCHASE_INFO = APT_PURCHASE; }
	else if (purchase_type == "back_up_care") { PURCHASE_INFO = BUC_PURCHASE; }
	else { PURCHASE_INFO = ""; }

	update_preview(CURRENT_FORM);
}

function update_preview(new_form) {
	let preview_div = document.getElementById("preview");
	if (new_form != null) { CURRENT_FORM = new_form; }
	CURRENT_TEXT = TEMPLATES[CURRENT_FORM]();
	preview_div.innerHTML = CURRENT_TEXT;
}

</script>




<style>
</style>