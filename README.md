# Calendly-Tracking-with-GTM-and-GA4
Track Calendly with Google Tag Manager and GA4


Listener code
To start tracking Calendly with Google Tag Manager, you must create a Custom HTML tag in your GTM container. Go to Tags > New > Custom HTML and paste the following code:

<script>
window.dataLayer = window.dataLayer ||[];
window.addEventListener('message',
  function(e) {
    if (e.data.event && e.data.event.indexOf('calendly') === 0) {
      window.dataLayer.push({
        'event' : 'calendly',
        'calendly_event' : e.data.event.split('.')[1]
      });
    }
  }
);
</script>



Track Calendly with Google Tag Manager and GA4
Updated: October 2nd, 2023

If you landed on this page, you (most likely) have embedded a Calendly calendar on your website. People land on your website, they can schedule appointments, and you would like to see that data in your analytics (e.g. Google Analytics 4).

If my guess was correct, you have come to the right place. In this blog post, I will explain how to track Calendly with Google Tag Manager, and then we will send data to Google Analytics 4 as events.


Table of contents
– Hide table of contents –

Before we continue
What kind of interactions can we track?
Listener code
Custom event trigger and Data Layer Variable
Create a Google Analytics 4 tag
Let’s test
Final words
 

Before we continue
In this blog post, I presume you have at least some basic knowledge about Google Tag Manager. If not, then read this tutorial first. And if you want to become a power GTM user, take a look at my courses.

 

Video tutorial
If you prefer video content, here’s a tutorial from my Youtube channel.


 

Google Tag Manager template
I also prepared a Google Tag Manager container template (a.k.a. recipe) to save you some time. You can download it here.

 

What kind of interactions can we track?
You will be able to capture the following events:

#1. When the profile page is viewed (meaning that someone lands on a page where your calendly calendar is embedded and loaded)



#2. When someone views an event type in your embedded calendar. For example, by clicking this one:



#3. When someone selects a date and time



#4. When someone schedules an event



Note: the solution that I explain in this blog post will not give you more granular data (like what exact time/date was selected or what kind of event type was viewed/scheduled). I know it would be nice to have more data, but that’s just what the official documentation of Calendly offers.

This method is good for general tracking (to know whether visitors look and schedule any events in your calendar).

 

Listener code
To start tracking Calendly with Google Tag Manager, you must create a Custom HTML tag in your GTM container. Go to Tags > New > Custom HTML and paste the following code:

<script>
window.dataLayer = window.dataLayer ||[];
window.addEventListener('message',
  function(e) {
    if (e.data.event && e.data.event.indexOf('calendly') === 0) {
      window.dataLayer.push({
        'event' : 'calendly',
        'calendly_event' : e.data.event.split('.')[1]
      });
    }
  }
);
</script>
This code is a listener that will be looking for Calendly events on a page (that are dispatched by the embedded calendar) and then will make them available in the Data Layer. It will push one of four events:

profile_page_viewed – when the profile page was viewed
event_type_viewed – when event type page was viewed
date_and_time_selected – when the invitee selected the date and time
event_scheduled – when the invitee successfully booked a meeting
In the triggering section of a tag, click anywhere and select the All Pages trigger. If your Calendly calendar is available only on certain pages, then you could create a more precise Pageview trigger where the condition is Page URL contains XXXX (replace XXX with the URL of the page where the calendar is embedded).


![image](https://github.com/xeniusdigital/Calendly-Tracking-with-GTM-and-GA4/assets/5832613/4b03760d-2622-4fc1-b60d-4e16f2d53204)


Custom event trigger and Data Layer Variable
Later in this blog post, we will create a Google Analytics 4 event tag to send the data to GA. But we need to define when that data should be sent.

In our case, that is when the ‘calendly‘ event is visible in the preview mode. To do that, we have to create a Custom Event trigger. In Google Tag Manager, go to Triggers > New > Custom Event and enter the following configuration.

![image](https://github.com/xeniusdigital/Calendly-Tracking-with-GTM-and-GA4/assets/5832613/05610d22-23cb-4002-a3bf-5a9cf3c6fc00)

Then let’s create a data layer variable to let us know what event happened. Was it profile_page_viewed  or event_scheduled? Or maybe something else?

Go to Variables > New > Data Layer variable and enter the following settings:

![image](https://github.com/xeniusdigital/Calendly-Tracking-with-GTM-and-GA4/assets/5832613/05b56432-7911-478d-afa8-758d2674c771)

Create a Google Analytics 4 tag
In this blog post, I presume that you already have the GA4 configuration tag in your container, and you know what it does. If you don’t, read this tutorial first.

Now, the time has come to send Calendly events to Google Analytics 4. In Google Tag Manager, go to Tags > New > Google Analytics > GA4 event tag.

Enter measurement ID.

Names could be calendar_profile_page_viewed or calendar_event_scheduled. Having unique event names is convenient for analysis like Path exploration. Also, in the list of events, you can clearly and quickly see what kind of calendar event it was.

If this naming convention works for you, your Ga4 event tag could look like this:

![image](https://github.com/xeniusdigital/Calendly-Tracking-with-GTM-and-GA4/assets/5832613/ab6e9a30-d2be-4d51-b1ac-06e33f0dbc97)

In the triggering section of the GA4 event tag, click anywhere and then select the custom event trigger you have just created. The final configuration of the tag can look like this:

![image](https://github.com/xeniusdigital/Calendly-Tracking-with-GTM-and-GA4/assets/5832613/0dad3339-ce43-438a-81a5-6bfa585c0174)

Let’s test
Save the tag, and click the preview button in the GTM interface (to refresh the preview mode). The page with the embedded calendar will reload.

![image](https://github.com/xeniusdigital/Calendly-Tracking-with-GTM-and-GA4/assets/5832613/f597758e-6b2e-49b5-8306-018cfafcec48)

![image](https://github.com/xeniusdigital/Calendly-Tracking-with-GTM-and-GA4/assets/5832613/8eacc920-e744-4432-8bfc-3fd3ab4e6ad0)

![image](https://github.com/xeniusdigital/Calendly-Tracking-with-GTM-and-GA4/assets/5832613/a5d6fe9b-d729-4b92-8c23-92b49037b3b5)






https://www.analyticsmania.com/post/how-to-track-calendly-with-google-tag-manager-and-google-analytics-4/


