# ios_twitterSdk_NO_UIWebView

To use the twitter SDK, you need to add these codes to the applicationWillResignActive method of AppDelegate.m

The purpose is to solve the problem of  iOS12 system webview is shown after confirm from the twitter app.

@property (nonatomic, assign) UIBackgroundTaskIdentifier taskIdentifier;

- (void)applicationWillResignActive:(UIApplication *)application
{
    
    if (self.taskIdentifier != UIBackgroundTaskInvalid) 
    {
        [application endBackgroundTask:self.taskIdentifier];
        self.taskIdentifier = UIBackgroundTaskInvalid;
    }
    __weak typeof(self) weakSelf = self;
    self.taskIdentifier = [application beginBackgroundTaskWithName:nil expirationHandler:^{
        [application endBackgroundTask:weakSelf.taskIdentifier];
        weakSelf.taskIdentifier = UIBackgroundTaskInvalid;
      }];
}

