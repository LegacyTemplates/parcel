# parcel

.NET Core 2.1 Parcel TypeScript Bootstrap App

[![](https://raw.githubusercontent.com/ServiceStack/Assets/master/csharp-templates/parcel.png)](http://parcel.web-templates.io/)

> Browse [source code](https://github.com/NetCoreTemplates/parcel), view live demo [parcel.web-templates.io](http://parcel.web-templates.io) and install with [dotnet-new](http://docs.servicestack.net/dotnet-new):

    $ npm install -g @servicestack/cli

    $ dotnet-new parcel ProjectName

## About

[https://parceljs.org](Parcel) provides the simplest out of the box development experience for developing npm-powered Web Apps which is pre-configured with [popular auto transforms](https://parceljs.org/transforms.html) for developing modern Web Apps. Parcel works by inspecting your `*.html` files to find all its dependencies which it automatically monitors for changes and bundles using advanced minification and bundling techniques.

To enable a pleasant development experience this template is pre-configured with the latest version of TypeScript enabling access to the latest ES7/TypeScript features.

This template starts from a clean slate which does not use any of the [popular JavaScript framework templates](https://github.com/NetCoreTemplates) making it ideal when wanting to use other [micro JS libraries](http://microjs.com) that can be referenced using a simple script include.

Or you can [develop without a JS framework](https://twitter.com/mislav/status/1022058279000842240), e.g. [index.ts](https://github.com/NetCoreTemplates/parcel/blob/master/MyApp/src/index.ts) uses TypeScript with the native HTML DOM APIs for its functionality:

```ts
import { client } from "./shared";
import { Hello } from "./dtos";

const result = document.querySelector("#result")!;

document.querySelector("#Name")!.addEventListener("input", async e => {
  const value = (e.target as HTMLInputElement).value;
  if (value != "") {
    const request = new Hello();
    request.name = value;
    const response = await client.get(request);
    result.innerHTML = response.result;
  } else {
    result.innerHTML = "";
  }
});
```

## Development workflow

If this is the first time using Parcel, you will need to install its global CLI:

    $ npm install -g parcel-bundler

Our recommendation during development is to run the `dev` npm script or Gulp task and leave it running in the background:

    $ npm run dev

This initially generates a full development build of your Web App then stays running in the background to process files as they're changed. This enables the normal dev workflow of running your ASP.NET Web App, saving changes locally which are then reloaded using ServiceStack's built-in hot reloading. Alternatively hitting `F5` will refresh the page and view the latest changes.

Each change updates the output dev resources so even if you stop the dev task your Web App remains in a working state that's viewable when running the ASP.NET Web App.

### Watched .NET Core builds

.NET Core projects can also benefit from Live Coding using dotnet watch which performs a “watched build” where it automatically stops, recompiles and restarts your .NET Core App when it detects source file changes. You can start a watched build from the command-line with:

    $ dotnet watch run

### Create a production build

Run the `build` npm script or gulp task to generate a static production build of your App saved to your .NET App's `/wwwroot` folder:

    $ npm run build

This will let you run the production build of your App that's hosted by your .NET App.

### Updating Server TypeScript DTOs

Run the `dtos` npm script or Gulp task to update your server dtos in `/src/dtos.ts`:

    $ npm run dtos

### Deployments

When your App is ready to deploy, run the `publish` npm (or Gulp) script to package your App for deployment:

    $ npm run publish

Which will create a production build of your App which then runs `dotnet publish -c Release` to Publish a Release build of your App in the `/bin/netcoreapp2.1/publish` folder which can then copied to remote server or an included in a Docker container to deploy your App.

