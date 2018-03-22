# Front End

Wrapping a feature in a toggle on the frontend is very straightforward.

If you want to wrap only one element on a page in a feature toggle called
`new_feature` simply do as follows:

```
<FeatureFlag name='new_feature'>
  <div>
    My very interesting feature.
  </div>
</FeatureFlag>
```

If you want to wrap a whole page in a feature flag and redirect to a 404 for
people who do not have that feature do this:

```
<FeatureFlag name='new_feature' redirect>
  <body
    This whole page will redirect if you don't have the feature turned on because the "redirect" flag was
    called.
  </body>
</FeatureFlag>
```

If you want an element to show **ONLY** when a feature is `TOGGLED OFF` and you
**DO NOT** want it to show when the feature is `TOGGLED ON` do this:

```
<FeatureFlag name='new_feature' toggledOff>
  <body
    Some old feature you only want to show to people who don't have the new feature yet.
  </body>
</FeatureFlag>
```

# Backend

Adding feature toggles on the backend is even more straightforward.

```
if Flipper.enabled?(:new_feature)
  puts "Do this code"
else
  puts "Do this instead"
end
```

# Adding the feature to flipper

## Code - Preferred for new features

1. Add your new feature name to the `TOGGLED_FEATURES` array in `slingshot/config/flipper.rb`
2. Restart the app
3. Your new feature will be added to the features list in flipper and will be
   turned on ONLY for developers.

You can later turn the feature on for the 'internal_users' group or other users
by navigating to the /flipper endpoint.

## GUI

Simply navigate to https://slingshot.tryadhawk.com/flipper/features (port 3000
on localhost). Follow the on-screen instructions to create your new flag.
Remember, feature flags should be snake_case. Your feature will still be off by
default. You can turn it on for user groups, a percentage of users or a
percentage of the time. You can also just turn it on for everyone.
