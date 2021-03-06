# collector-react

The feedback collector is a simple form that helps you quickly gather user feedback from your own website or web app. When people fill out the form, their entries are saved as notes in [Dovetail](https://dovetailapp.com). You’ll need a project on Dovetail, along with its collector ID (found in [collector settings](https://dovetailapp.com/help/form-code)).

![Screenshot of collector-react](https://raw.githubusercontent.com/heydovetail/collector-react/master/img/screenshot.png)

## Installation

```bash
npm i @heydovetail/collector-react
```

## Example implementation

```jsx
import { Collector } from "@heydovetail/collector-react"
import * as React from "react";

interface State {
  feedback: boolean;
}

class Example extends React.Component<{}, State> {
  public state: State = { feedback: false };

  public render() {
    return (
      <div>
        <button onClick={() => { this.setState({ feedback: true }); }}>Send feedback</button>

        {this.state.feedback ? (
          <Collector
            collectorId="yourCollectorId"
            defaultEntries={{ email: "foo@example.com" }}
            onDismiss={(sent: boolean) => {
              sent ? console.log("Feedback sent!") : this.setState({ feedback: false });
            }}
            metadata={{ browser: navigator.userAgent }}
          />
        ) : null}
      </div>
    );
  }
}
```

## Props

```jsx
export interface Props {
  // Collector ID from Dovetail.
  // Find this in your project’s collector settings.
  collectorId: string;

  // Optional key:value pairs for setting default data.
  // e.g. prefill user’s name and email if they’re logged in.
  defaultEntries?: { [key: string]: string };

  // Optional domain for where to fetch the dialog.
  // Defaults to dovetailapp.com.
  domain?: string;

  // Optional key:value pairs for passing extra information.
  // e.g. store browser version, local time, etc.
  metadata?: { [key: string]: string };

  // Called when the user clicks the ‘X’ icon to close the dialog
  // or the ‘Done’ button after successfully sending the form.
  //
  // Returns true or false depending on whether feedback was sucessfully sent
  // or false if the user just closed the dialog without sending feedback.
  onDismiss: (sent: boolean) => void;
}
```

## Configuration

Configure the look & feel in your Dovetail project. You can customize the color, text, where entries are saved, and more. Read the [customization documentation](https://dovetailapp.com/help/form-customize) for more information.

## Build status

[![CircleCI](https://circleci.com/gh/heydovetail/collector-react.svg?style=svg)](https://circleci.com/gh/heydovetail/collector-react)
