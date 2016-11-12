A collection of snippets to get start using Mixpanel Analytics to manage User Behavior patterns.

https://mixpanel.com/

Meteor add okgrow:analytics package
https://github.com/okgrow/analytics

Currently supports


    Amplitude
    Chartbeat
    comScore
    Google Analytics
    HubSpot
    Intercom
    Keen IO
    KISSmetrics
    Mixpanel
    Quantcast
    Segment.io


Get your Token, API key and API secret -- but keep these safe from crawlers and differentiate between production and development builds. 

For an exaustive list of properties see

https://mixpanel.com/help/questions/articles/what-properties-do-mixpanels-libraries-store-by-default

##Example Settings.json

{
  "public": {
    "analyticsSettings": {
      // Add your analytics tracking ids here (remove this line before running)
      "Google Analytics" : {"trackingId": "Your tracking ID"},
      "Amplitude"        : {"apiKey": "..."},
      "Chartbeat"        : {"uid": "..."},
      "comScore"         : {"c2": "..."},
      "HubSpot"          : {"portalId": "..."},
      "Intercom"         : {"appId": "..."},
      "Keen IO"          : {"projectId": "...", "writeKey": "..."},
      "KISSmetrics"      : {"apiKey": "..."},
      "Mixpanel"         : {"token":  "...", "people": true},
      "Quantcast"        : {"pCode": "..."},
      "Segment.io"       : {"apiKey": "..."}
    }
  },
  "private": {...}
}




The key for performance will seek to collect --

1) Who did what and @ what time?
2) What came next and @ what time? 
3) @ what time boundaries did who get stuck onboarding between ?
4) What defines "stuck" and does it link to support services (SaaS, Rank, API, BS) and how will the issue be dissolved/solved to exact a solution.
5) What conclusion were drawn about decisions and how did the data identify influential onboarding sections that deliver scope to specific tracked goals. 


##Identify

<header>
<a href="/signup" class="signup">Signup</a>
</header> 

Template.header.events({
  'click .signup' () {
    AnalyticsService.track( 'Clicked the signup link' ); 
  }
});

Meteor.loginWithPassword( email, password, ( error ) => {
  if ( error ) {
    Bert.alert( error.reason, 'warning' );
  } else {
    Bert.alert( 'Logged in!', 'success' );

    analytics.identify( Meteor.userId(), {
      email: Meteor.user().emails[0].address,
      name: Meteor.user().profile.name
    });
  }
});

Accounts.createUser( user, ( error ) => {
  if ( error ) {
    Bert.alert( error.reason, 'danger' );
  } else {
    Bert.alert( 'Welcome!', 'success' );

    analytics.identify( Meteor.userId(), {
      email: Meteor.user().emails[0].address,
      name: Meteor.user().profile.name
    });
  }
});


##Track

<template name="Sourcecalls">
  <h3>Example Event Local</h3>

  <a href="#" class="btn btn-success">Create a New input</a>
  <a href="#" class="btn btn-danger">Action Delete </a>
  <a href="#" class="btn btn-warning">Action Edit </a>
  <a href="#" class="btn btn-info">Action Confirm</a>
  <a href="#" class="btn btn-info">Action Cancel</a>
  <a href="#" class="btn btn-default">Action Close</a>
</template>

Template.Sourcecalls.events({
'click .btn-default' () {
    analytics.track( 'closed', {
      title: closed element label

//using revenue tied to a purchase you can simple track one-off buying 
analytics.track ('disposable_income', {
      revenue: 36567.41
    });

    // Just to confirm the event. Not necessary.
    Bert.alert( 'Element was closed!', 'default' );
  }
});
