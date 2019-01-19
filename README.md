# parcel

.NET Core 2.1 Parcel TypeScript Bootstrap App

[![](https://raw.githubusercontent.com/ServiceStack/Assets/master/csharp-templates/parcel.png)](http://parcel.web-templates.io/)

> Browse [source code](https://github.com/NetCoreTemplates/parcel), view live demo [parcel.web-templates.io](http://parcel.web-templates.io) and install with [dotnet-new](http://docs.servicestack.net/dotnet-new):

    $ dotnet tool install -g web

    $ web new parcel ProjectName

## About

[Parcel](https://parceljs.org) aims to provide the simplest config-free out-of-the-box development experience for developing modern npm-powered 
Web Apps by getting out of your way and letting you develop Websites without any regard for bundling solution or JS Framework. To enlist its 
functionality you just point it to your home page:

    $ parcel index.html

This starts a Live Hot Reload Server which inspects all linked `*.html`, script and stylesheet resources to find all dependencies which it automatically 
monitors for changes where it will automatically rebuild and reload your webpage. Then when it's time for deployment you can perform a production build
for your website with the `build` command:

    $ parcel build index.html

Where it creates an optimized bundle using advanced minification, compilation and bundling techniques. Despite its instant utility and zero configuration,
it comes pre-configured with [popular auto transforms](https://parceljs.org/transforms.html) for developing modern Web Apps which lets you utilize 
PostCSS transforms and advanced transpilers like TypeScript which this Template uses to enable a pleasant development experience by enabling access to
the latest ES7/TypeScript language features.

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

This template includes customizatinos for integrating with .NET Core project conventions and [ServiceStack Templates](http://templates.servicestack.net) for its 
dynamic Web Pages and server-side HTML rendering.

## Development workflow

If this is the first time using Parcel, you will need to install its global CLI:

    $ npm install -g parcel-bundler

Our recommendation during development is to run the `dev` npm script and leave it running in the background:

    $ npm run dev

This initially generates a full development build of your Web App then stays running in the background to process files as they're changed. This enables the normal dev workflow of running your ASP.NET Web App, saving changes locally which are then reloaded using ServiceStack's built-in hot reloading. Alternatively hitting `F5` will refresh the page and view the latest changes.

Each change updates the output dev resources so even if you stop the dev task your Web App remains in a working state that's viewable when running the ASP.NET Web App.

### Watched .NET Core builds

.NET Core projects can also benefit from Live Coding using dotnet watch which performs a “watched build” where it automatically stops, recompiles and restarts your .NET Core App when it detects source file changes. You can start a watched build from the command-line with:

    $ dotnet watch run

### Create a production build

Run the `build` npm script to generate a static production build of your App saved to your .NET App's `/wwwroot` folder:

    $ npm run build

This will let you run the production build of your App that's hosted by your .NET App.

### Updating Server TypeScript DTOs

Run the `dtos` npm script to update your server dtos in `/src/dtos.ts`:

    $ npm run dtos

### Deployments

When your App is ready to deploy, run the `publish` npm (or Gulp) script to package your App for deployment:

    $ npm run publish

Which will create a production build of your App which then runs `dotnet publish -c Release` to Publish a Release build of your App in the `/bin/netcoreapp2.1/publish` folder which can then copied to remote server or an included in a Docker container to deploy your App.

