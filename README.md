# Coffee Beans Selling App

This project is a B2B application connecting coffee retailers and farmers, providing a platform for seamless transactions and communications. The app is built using HTML, JavaScript, and Asgardeo Auth SPA SDK for authentication.

## Getting Started

### Register an Application

1. Create an Asgardeo account and organization: [Asgardeo Signup](https://asgardeo.io/signup).
2. Register a Single-Page Application in Asgardeo.
3. Add `https://localhost:3000` as a Redirect URL and Allowed Origin.

### Configuring the Sample

1. Update the `authConfig` object in `index.html` with your app details.

```js
const authConfig = {
    clientID: "<ADD_CLIENT_ID_HERE>",
    signInRedirectURL: "https://localhost:3000",
    baseUrl: "https://api.asgardeo.io/t/coffeeapp",
    scope: ["openid", "profile"]
};

The app should open at https://localhost:3000. If you encounter an invalid-certificate error, type thisisunsafe to continue.

### Changing the Development Server Port

1. Update the PORT in the .env file in the app root.
2. Update the signInRedirectURL & signOutRedirectURL in the authConfig object in index.html.
3. Update the Authorized Redirect URL and Allowed Origins in the Asgardeo Console.
4. Configuring ACR-based Adaptive Authentication
5. Follow the guide to configure ACR-based adaptive authentication in Asgardeo: ACR-based Adaptive Authentication.
6. Use the provided JavaScript function to set up conditional authentication.

```js
var supportedAcrValues = ['acr1', 'acr2'];

var onLoginRequest = function (context) {
    var selectedAcr = selectAcrFrom(context, supportedAcrValues);
    Log.info('--------------- ACR selected: ' + selectedAcr);
    context.selectedAcr = selectedAcr;
    switch (selectedAcr) {
        case supportedAcrValues[0]:
            executeStep(1, {
                onSuccess: function (context) {
                    var user = context.steps[1].subject;
                    user.claims["http://wso2.org/claims/acr"] = "acr1";
                }
            });
            break;
        case supportedAcrValues[1]:
            executeStep(1);
            executeStep(2, {
                onSuccess: function (context) {
                    var user = context.steps[1].subject;
                    user.claims["http://wso2.org/claims/acr"] = "acr2";
                }
            });
            break;
        default:
            executeStep(1, {
                onSuccess: function (context) {
                    var user = context.steps[1].subject;
                    user.claims["http://wso2.org/claims/acr"] = "acr1";
                }
            });
    }
};
```

### Branding
Customize the login UI using Asgardeo’s Branding section or the Branding AI feature.

### User Management
Add users through the User Management section in Asgardeo.

### Insights
Check the number of logins and registrations in the Insights section of Asgardeo.
