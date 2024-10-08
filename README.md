# Transaction Analyzer Manual

## Overview

This project is an extension of [PlutoWallet](https://play.google.com/store/apps/details?id=com.rostislavlitovkin.plutowallet&hl=cs) crypto wallet. It adds analysis of your transaction and a pop-up window of expected events before confirmation. It is used for making your transaction more secure and prevent possible errors.

## How it works?

There are two parts to Transaction Analyzer. The local **Client in C#** language and a **Webserver running Chopsticks**. The [Chopsticks](https://github.com/AcalaNetwork/chopsticks) tool developed by Acala is used to copy the Blockchain code, simulate the transaction on the server-side copy and return the events resulting from the simulated transaction. The local Client is than used for looking throw the events and displaying them to the user before he can confirm his transaction.

**XCM is also supported** and the events from the simulated transaction are collected from both blockchains participation in the XCM transaction.

## How to Run?

First we will need the **Server with Chopsticks** and than the **Client** to communicate with it.

### Server with Chopsticks

The Test Server is **already deployed** and ready to use on this adress: https://express-byrr9.ondigitalocean.app/.

To get the events resulted from the transaction, Client comunicates with the https://express-byrr9.ondigitalocean.app/get-extrinsic-events, which also expects request body in format defined in the client.

### C# Client

We recommend to use Visual Studio code editor from Microsoft. The detailed installation guide can be found [here](https://learn.microsoft.com/en-us/visualstudio/install/install-visual-studio?view=vs-2022).

Once installed, you should clone the PlutoWallet repository from Github and switch to `TransactionAnalyzer` branch. So in your preferred repository in console:

```
git clone https://github.com/RostislavLitovkin/PlutoWallet
git switch TransactionAnalyzer
```

Then open this cloned project in Visual Studio. You should see something like this:

![Alt Text](/images/opened_plutowallet.png)

Here you can navigate to the upper bar, where you go to **View >> Test Explorer**. A test explorer window should open and there you should find the **PlutoWalletTests >> PlutoWalletTests >> ChopsticksTests** tests.

![Alt Text](/images/tests_location.png)

If you double click any test under the **ChopsticksTests**, you will be able to find the source code for the test. If you `right-click` any test, like SimulateXcmCallAsync for instance, and click **Run**, the test runs and you will be able to see the resulting events of a XCM Transaction between Hydration and PolkadotAssetHub chains.

![Alt Text](/images/run_test.png)

## Transaction Analyzer in PlutoWallet

In the Plutowallet, the Analyzer code can be found in **Plutowallet.Model >> ChopsticksModel.cs**. There you can find the interfaces for the client-server communication and mainly the `ChopsticksModel.SimulateCallAsync` and `ChopsticksModel.SimulateXcmCallAsync` which facilitate the communication with Chopsticks run on Server.

Also in the **PlutoWallet >> Components >> TransactionAnalyzer**, you can find the UI Components used for displaying the analysis results.

## Conclusion

Now you have created a local copy of the PlutoWallet on your device, throw the test run a Chopsticks on the server and fetched the resulting events.
