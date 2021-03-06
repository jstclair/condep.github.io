---
layout: doc
title: WindowsServiceWithInstaller
permalink: /docs/3-0/operations/deployment/windows-service-with-installer/
---

WindowsServiceWithInstaller
===========================

Will deploy the given Windows Service to remote server, using the build-in installer in the service.

## Syntax

{% highlight csharp %}
WindowsServiceWithInstaller(
  string serviceName, 
  string displayName, 
  string sourceDir, 
  string destDir, 
  string relativeExePath, 
  string installerParams
)
{% endhighlight %}
{% highlight csharp %}
WindowsService(
  string serviceName, 
  string displayName, 
  string sourceDir, 
  string destDir, 
  string relativeExePath, 
  string installerParams,
  Action<IOfferWindowsServiceOptions> options
)
{% endhighlight %}

<table>
	<thead>
		<tr>
			<th>Parameter</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>serviceName</td>
			<td>Name of the service</td>
		</tr>
		<tr>
			<td>displayName</td>
			<td>Display name of the service</td>
		</tr>
		<tr>
			<td>sourceDir</td>
			<td>The client directory where the files for the service are located</td>
		</tr>
		<tr>
			<td>destDir</td>
			<td>The destination directory where the service will be deployed to the server</td>
		</tr>
		<tr>
			<td>relativeExePath</td>
			<td>The path or just the name (if located on root) of the executable for the service</td>
		</tr>
		<tr>
			<td>installerParams</td>
			<td>Any parameters needed by the installer</td>
		</tr>
		<tr>
			<td>options</td>
			<td>See <a href="../../options/IOfferWindowsServiceOptions/">IOfferWindowsServiceOptions</a></td>
		</tr>
	</tbody>
</table>

## Code Example

{% highlight csharp %}
public class MyRemoteArtifact : Artifact.Remote
{
  public override void Configure(IOfferRemoteOperations server, ConDepSettings settings)
  {
    server.Deploy
      .WindowsServiceWithInstaller(
        serviceName: "MyService",
        displayName: "My Service",
        sourceDir: @"C:\services\myservice",
        destDir: @"E:\services\myservice",
        relativeExePath: @"myservice.exe",
        installerParams: "/myParam someValue",
        options: opt => opt
          .UserName(@"mydomain\myuser")
          .Password("my$uper$ecretP@ssw0rd")
      );
  }
}
{% endhighlight %}
