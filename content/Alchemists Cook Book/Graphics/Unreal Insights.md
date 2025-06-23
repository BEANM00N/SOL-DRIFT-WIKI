# Unreal Insights

Profile your project with Unreal Insights.

![Unreal Insights](https://dev.epicgames.com/community/api/documentation/image/6ead2311-df12-4898-9d2a-90efcad65e4c?resizing_type=fill&width=1920&height=335)

**Unreal Insights** is a telemetry capture and analysis suite that can capture events from your project at high data rates. Unreal Insights helps you identify areas of data that might require optimization.

The major components of Unreal Insights are:

- **Trace events**, which contain `EventName` and `FieldName` parameters to define an event and specify a field that the event should include.
- The **Unreal Trace Server**, which records and saves traces from the application.
- **Unreal Insights**, which analyzes and visualizes the data.

![insights-diagram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6278d1d2-3370-468e-bd3f-c8e8b33514e3/insightsdiagram.jpg)

Visualization of the major components of the Unreal Insights framework.

Trace sessions are self-describing, and compatible with different engine release versions. They are stored in `.utrace` files. Any companion data that is generated is stored in `.ucache` files located within the same directory as your trace files.

## Setting Up Unreal Insights

### Launch From Editor

To start Unreal Insights from the **Unreal Editor**, navigate to the **Trace/Insights Status Bar Widget** located in the bottom toolbar of the Editor.

![insights-widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef8ed796-9997-41fc-b39a-e6407d545d2f/insightswidget.png)

When you run a Trace to profile your project data, you can choose from multiple workflow options that vary depending on your Unreal Engine Build and Operating System. For more information about these workflow options, see the following pages:

- [Trace](https://dev.epicgames.com/documentation/en-us/unreal-engine/trace-in-unreal-engine-5?application_version=5.3)
- [Trace Quick Start Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/trace-quick-start-guide-in-unreal-engine?application_version=5.3)

### Launch a prebuild of Unreal Insights

If you installed a binary version of Unreal Engine you should have a compiled version of Unreal Insights located in the following directory:

```cpp
Engine\Binaries[Platform]\UnrealInsights[.exe] 	
```

### Build From Source

If you don't have a binary version of the engine installed, or you want to compile Unreal Insights from source, you can use the following options:

- **Using an Integrated Development Enviroment (IDE)**. Find the UnrealInsights target located in the Programs folder.
- **From the command prompt**. In your engine installation folder build Unreal Insights using the Unreal Build Tool:

On Windows:

```cpp
Engine/Build/BatchFiles/RunUBT.bat UnrealInsights Win64 Development
```

On Linux or Mac:

```cpp
./Engine/Build/BatchFiles/RunUBT.sh UnrealInsights [Linux|Mac] Development
```

## Trace

**Trace** is a structured logging framework for tracing instrumentation events from a running process. The **Unreal Trace Server** runs in the background as a single server instance and can be shared between multiple projects or branches. It is an optimized program that has minimal impact on performance and does not include a User Interface.

The **Trace Server** is launched automatically by a separate server process executable, `UnrealTraceServer.exe`, which is located in the `Engine/Binaries/Win64` directory folder.

The **Trace Server** has two components:

- The **Trace Recorder** listens on port 1981 for incoming trace connections and records the live trace stream.
- The **Trace Store** stores the recorded traces as files in a folder. It watches this folder for changes and exposes the list of available traces to Unreal Insights UI.

The **Trace Server** stores configuration and log files in:

- Windows: `%LOCALAPPDATA%/UnrealEngine/Common/UnrealTrace`
- MacOS: `~/UnrealEngine/UnrealTrace`
- Linux: `~/UnrealEngine/UnrealTrace`

The default `Store` folder is created here.

For additional documentation see the following pages:

- [Trace](https://dev.epicgames.com/documentation/en-us/unreal-engine/trace-in-unreal-engine-5?application_version=5.3)
- [Trace Quick Start Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/trace-quick-start-guide-in-unreal-engine?application_version=5.3)
- [Trace Developer Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/developer-guide-to-tracing-in-unreal-engine?application_version=5.3)

### Shut Down Trace Server

The server can be shut down using the "kill" command:

`> UnrealTraceServer kill`

### Configuring the Unreal Trace Server

You can configure the Unreal Trace Server to add additional directories to scan for trace files like the download folder or the profiling directory of a specific project. In Unreal Insights, you can control these settings to:

- Set the trace store directory. This is the location where new traces are saved.

[![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33730d59-179a-4334-9d89-fbe502e7d5a1/settracedirectory.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33730d59-179a-4334-9d89-fbe502e7d5a1/settracedirectory.png)

- Set additional trace directories and additional sources for trace files, for example, your user Download folder.

[![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dcc23dc-3464-4d0d-8472-2d5aec7e964d/colorfilter.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dcc23dc-3464-4d0d-8472-2d5aec7e964d/colorfilter.png)

When configured with additional watch folders, multiple traces, and their corresponding trace file origin will be displayed with the associated color

- The Unreal Trace Server can store settings persistently while your computer is shut down or restarted.

As of UE 5.3, the Unreal Trace Server is enabled for all desktop platforms. This deprecates the store which was hosted in Unreal Insights for Linux and Mac.

Follow the steps below to Configure the Unreal Trace Server.

1. Open Unreal Insights. This will start the Unreal Trace Server, if not already running, on Windows, Mac, or Linux
    
2. Click on the **Manage store settings** dropdown button then modify the default store directory by clicking the "Set Trace Store directory" button. When starting a new trace the file will be stored in this directory.
    
    [![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b37f3659-60e2-4b46-bf9a-bbbb66fd975d/managestoresettings.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b37f3659-60e2-4b46-bf9a-bbbb66fd975d/managestoresettings.png)
    
3. The old trace store directory is automatically added to watch folders.
    
4. You can add one or more watch folders by clicking the **Add directory** button. If the new folder contains trace files they will appear in the session list with an icon colored by a unique color.
    
    [![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d94ea78-5eb1-455a-b9f4-5c251b85d4a2/adddirectory.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d94ea78-5eb1-455a-b9f4-5c251b85d4a2/adddirectory.png)
    

## Unreal Insights Session Browser

The **Unreal Insights Session Browser** is an interface to observe trace data. To launch the browser, navigate to the bottom toolbar, and click **Trace** > **Insights** > **Unreal Insights** (**Session Browser**.)

### Trace Store

The **Trace Store** is an interface for you to observe and manage all of your stored Trace Sessions. The recorded traces are stored as files in a folder and Unreal Insights watches this folder for any data changes and then exposes the list of available traces to Unreal Insights UI.

![session-browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95d39834-6e25-4075-b3bb-66f0544fc6ef/sessionbrowser.png)

|Numeric Index|Category|Description|
|---|---|---|
|(1)|**Trace Store Panel**|Opens and manages your trace files for analysis.|
|(2)|**Trace Story Directory**|Displays and Opens the directory path to the Trace Sessions.|
|(3)|**Trace Sessions**|Lists pre-recorded sessions that you can load for analysis. These correspond to the `.utrace` files in your Trace Store Directory. You can right-click a Trace Session to Rename or Delete it. Alternatively, you can use shortcut keys. Click the Trace Session and press **F2** to rename, or **Del** to delete it.|
|(4)|**Session Filters**|Sort your trace files into **Platform**, **App Name**, **Config**, **Target**, and **Branch** categories.|
|(5)|**Search Bar**|Filters your searches by command line or name.|
|(6)|**Connection Tab**|Sets up connections to a remote trace server.|

### Connection Tab

The connection tab allows you to connect to a running game or editor with a trace server. It features multiple options to change your connection settings.

![connection-tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7268cfc-b87a-4fa6-8423-af4461547757/connectiontab.png)

|Numeric Index|Category|Description|
|---|---|---|
|(6)|**Connection Tab**|Manages the connection between a remotely running game or editor to a trace server.|
|(7)|**Trace Recorder IP address**|The IP address of the trace server.|
|(8)|**Running Instance IP address**|The IP address of the project(running instance) that connects with the trace server to begin tracing data.|
|(9)|**Initial channels**|A field to specify the list of trace channels to be enabled when the trace connection begins analyzing data.|

### Load a Trace for Analysis

There are multiple options to choose to load a Trace for Analysis. You can:

- Double-click any trace session in the Unreal Insights Browser.
- Select a trace session and click **Open Trace**.
- Search for `.utrace` files in other locations by using the **Open Trace** drop-down arrow.
- Start an analysis of a respective trace file immediately, drag and drop a .utrace file from Explorer over the Unreal Insights window.

![trace-drop-down-menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd2b2004-18eb-49df-9f02-f931e1165492/tracedropdown.png)

### Live Connect

If a live Trace session connects to the tool, it also appears in the list. Live sessions display the word **LIVE** in the status column and update in real-time while you analyze them. Otherwise, they are identical to pre-recorded sessions.

![live-connect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1574b08e-abb3-46cf-b2fd-b4e18dc2a1c6/liveconnect.png)

The tool can connect to multiple sessions at the same time, and it automatically records data for all of them as the data streams in. To analyze these sessions in real-time, load them from the list the same way you load pre-recorded sessions.

## Timing Insights Window

The **Timing Insights** window collects performance data. It displays the data for **CPU** and **GPU** tracks. These tracks feature multiple sub-menus to help you sort and visualize the various processing tasks and the amount of time your project spends on executing them.

![timing-insights-window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bed5a79e-3a74-4bd8-b060-24a62bf2f524/timinginsightswindow.jpg)

The Timing Insights window features the Frames panel (1), the Timing panel filters (2), the Timing panel (3), the Log panel (4),Timers and Counters tabs (5) and the Callers and Callees panels (6).

See the [Timing Insights](https://dev.epicgames.com/documentation/en-us/unreal-engine/timing-insights-in-unreal-engine-5?application_version=5.3)

## Memory Insights

The **Memory Insights** component allows you to investigate memory usage and call stack tracing in your project.

[![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f89726a-fa3b-45c8-9f6b-a87b8ce12f2e/memoryinsightswindow.jpg)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f89726a-fa3b-45c8-9f6b-a87b8ce12f2e/memoryinsightswindow.jpg)

Memory Insights traces events for every allocation, reallocation, or free event that occurs during runtime, then reconstructs that memory usage pattern during analysis.

[![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6eedfe72-4b15-498f-a0f6-80eb8f3ef7ab/allocationtable.jpg)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6eedfe72-4b15-498f-a0f6-80eb8f3ef7ab/allocationtable.jpg)

See the [Memory Insights](https://dev.epicgames.com/documentation/en-us/unreal-engine/memory-insights-in-unreal-engine?application_version=5.3) documentation for instructions on how to set up, trace, query, and sort your data.

## Networking Insights

Unreal Insights includes **Networking Insights** to analyze, optimize and debug network traffic.

Refer to the [Networking Insights](https://dev.epicgames.com/documentation/en-us/unreal-engine/networking-insights-in-unreal-engine?application_version=5.3) for additional documentation.

## Slate Insights

**Slate Insights** extends Unreal Insights to help developers improve the performance of their UI. it provides tools to identify the root cause of a specific Slate and UMG update.

See [Slate Insights](https://dev.epicgames.com/documentation/en-us/unreal-engine/slate-insights-in-unreal-engine?application_version=5.3) for additional documentation.

## Asset Loading Insights

**Asset Loading Insights** provides a way to profile the amount of time it takes to load a project's assets into UnrealEngine. It can give you a detailed understanding of data sets per asset type. Asset Loading Insights is based on the data traced from the AssetLoadTime trace channel.

## Cooking Insights

**Unreal Cooking Insights** allows you to gather and display information about the way packages are cooked in your project. Long cooking times can significantly affect the productivity of teams that are working on larger projects. By displaying the time it takes to cook each package, you can observe which packages to focus your investigation into optimizing. See [Cooking Insights](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-cooking-insights-in-unreal-engine-5?application_version=5.3) for additional documentation.

## Reference

To get the most out of the many features that ship with **Unreal Insights**, You can customize your project's output with macros and command-line options.

Refer to the [Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-insights-reference-in-unreal-engine-5?application_version=5.3) for additional documentation.