---
Order: 30
Title: SetVariableNames Method
Description: Override the default names of the environment variables used by Cake.Recipe
---

Cake.Recipe is driven by [environment variables](./environment-variables).  These are used to store the sensitive information that is required during the build process.  For example, the username and password needed to send email, or the token required to access GitHub.

Cake.Recipe has default environment variable names for all the pieces of information that are required.  The expectation is that either locally on your own machine, or on the CI/CD pipeline that you are using, you set the values for all of the ones that you intend to use.  For example, if you want to send messages to Gitter when the build succeeds, you will need to set environment variables with the names required.

However, it may be necessary to change these environment variable names.  One example of when this is required is when you might be using Cake.Recipe on two completely separate projects.  In this scenario, you might need to set the Gitter Environment variables for both projects, but they may require different values.

As an example, lets say that you wanted to change the name of the environment variables that stored the Gitter credential information.  You could add something like the following to your [recipe.cake](./recipe-cake) file:

```csharp
Environment.SetVariableNames(gitterTokenVariable: "PROJECTA_GITTER_TOKEN", gitterRoomIdVariable: "PROJECTA_GITTER_ROOM_ID");
```

This would mean that when required, Cake.Recipe would check the machine which it is running on for environment variables names `PROJECTA_GITTER_TOKEN` and `PROJECTA_GITTER_ROOM_ID`, rather than the default of `GITTER_TOKEN` and `GITTER_ROOM_ID`.

There is another scenario where you might want to override the environment variable names when running locally on your own machine, but you might want to use the default variable names when running on a CI/CD system.  To facilitate that, you can do something similar to the following:

```csharp
if (BuildSystem.IsLocalBuild)
{
    Environment.SetVariableNames(gitterTokenVariable: "PROJECTA_GITTER_TOKEN", gitterRoomIdVariable: "PROJECTA_GITTER_ROOM_ID");
}
else
{
    Environment.SetVariableNames();
}
```

## Default Environment Variable Names Parameters

The `SetVariableNames` method uses the concept of optional parameters, in fact, all the parameters to the `SetVariableNames` method are optional.  To override a specific environment variable, you need to use a named parameter.  The following is a list of all the named parameters that can be used on the method.

### githubTokenVariable

Default value: `GITHUB_PAT`

### gitterTokenVariable

Default value: `GITTER_ROOM_ID`

### gitterRoomIdVariable

Default value: `GITTER_ROOM_ID`

### slackTokenVariable

Default value: `SLACK_TOKEN`

### slackChannelVariable

Default value: `SLACK_CHANNEL`

### twitterConsumerKeyVariable

Default value: `TWITTER_CONSUMER_KEY`

### twitterConsumerSecretVariable

Default value: `TWITTER_CONSUMER_SECRET`

### twitterAccessTokenVariable

Default value: `TWITTER_ACCESS_TOKEN`

### twitterAccessTokenSecretVariable

Default value: `TWITTER_ACCESS_TOKEN_SECRET`

### emailSmtpHost

Default value: `EMAIL_SMTPHOST`

### emailPort

Default value: `EMAIL_PORT`

### emailEnableSsl

Default value: `EMAIL_ENABLESSL`

### emailUserName

Default value: `EMAIL_USERNAME`

### emailPassword

Default value: `EMAIL_PASSWORD`

### appVeyorApiTokenVariable

Default value: `APPVEYOR_API_TOKEN`

### codecovRepoTokenVariable

Default value: `CODECOV_REPO_TOKEN`

### coverallsRepoTokenVariable

Default value: `COVERALLS_REPO_TOKEN`

### microsoftTeamsWebHookUrlVariable

Default value: `MICROSOFTTEAMS_WEBHOOKURL`

### transifexApiTokenVariable

Default value: `TRANSIFEX_API_TOKEN`

### wyamAccessTokenVariable

Default value: `WYAM_ACCESS_TOKEN`

### wyamDeployRemoteVariable

Default value: `WYAM_DEPLOY_REMOTE`

### wyamDeployBranchVariable

Default value: `WYAM_DEPLOY_BRANCH`
