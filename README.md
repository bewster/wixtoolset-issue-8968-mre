# WixBuildIssueMRE

This project is a Minimal Reproducible Example to accompany https://github.com/wixtoolset/issues/issues/8968.

`WinFormsApp2` is configured to target multiple frameworks, but only one is specified.

```
<TargetFrameworks>net8.0-windows</TargetFrameworks>
```

As a comparison `WinFormsApp1` is only targeting a single framework.

```
<TargetFramework>net8.0-windows</TargetFramework>
```

For the `Package1` WiX project both projects are referenced:

```
    <ProjectReference Include="..\WinFormsApp1\WinFormsApp1.csproj" />
    <ProjectReference Include="..\WinFormsApp2\WinFormsApp2.csproj">
      <TargetFrameworks>net8.0-windows</TargetFrameworks>
    </ProjectReference>
```

When building the solution, a build of the `WinFormsApp2` is triggered building `Package1`:

```
Build started at 20:54...
1>------ Build started: Project: WinFormsApp2, Configuration: Debug Any CPU ------
2>------ Build started: Project: WinFormsApp1, Configuration: Debug Any CPU ------
2>WinFormsApp1 -> D:\source\WixBuildIssueMRE\WinFormsApp1\bin\Debug\net8.0-windows\WinFormsApp1.dll
2>".NET-SDK Project Built"
1>WinFormsApp2 -> D:\source\WixBuildIssueMRE\WinFormsApp2\bin\Debug\net8.0-windows\WinFormsApp2.dll
1>".NET-SDK Multi-Targeted Project Built"
3>------ Build started: Project: Package1, Configuration: Debug x64 ------
3>WinFormsApp2 -> D:\source\WixBuildIssueMRE\WinFormsApp2\bin\Debug\net8.0-windows\WinFormsApp2.dll
3>".NET-SDK Multi-Targeted Project Built"
3>Package1 -> D:\source\WixBuildIssueMRE\Package1\bin\x64\Debug\en-US\Package1.msi
========== Build: 3 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
========== Build completed at 20:54 and took 10.477 seconds ==========
```
