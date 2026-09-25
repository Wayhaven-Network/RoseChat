![](https://imgur.com/IAyRti3.png)


RoseChat is a chat plugin that allows you to format chat with channels, colors, placeholders, emojis, and more!

### Documentation
Any and all information you need for the plugin should already be included [in our Wiki](https://github.com/Rosewood-Development/RoseChat/wiki)!

### Support
If there's anything we left out, you have a question, you want to report a bug, or anything else, please [join our Discord server](https://discord.gg/MgUsTBK).  We offer any and all support in our server.

### Server Compatibility
RoseChat is compatible with Spigot and any forks. We recommend using [Paper](https://papermc.io/) to run your server.  CraftBukkit servers will not be compatible with the plugin.

We support Minecraft versions **1.16.5** and newer running **Java 21**.

If you wish to use this plugin on a 1.16.5 server (newer versions do not need this), you will need to use [Paper](https://papermc.io/) (or a fork of Paper), Java 21, and add the flag `-DPaper.IgnoreJavaVersion=true` to your server's startup parameters.


___TO DO___
RoseChat RC-4 was built for an older Adventure API, while Purpur 1.21.11 uses a newer Adventure API that removed ClickEvent$Action$OpenUrl, causing RoseChat to crash when processing chat.


2. Search the source code for the old Adventure API:

grep -R "ClickEvent.Action" -n src

3. Find AdventureTokenDecorator.java and inspect around line 73.

4. Replace old Adventure 4 click-event code such as:

ClickEvent.Action.OpenUrl

with the Adventure 5 API:

ClickEvent.openUrl(url)

5. Search for other old Adventure API usages:

grep -R "ClickEvent.Action" -n src
grep -R "HoverEvent.Action" -n src
grep -R "ClickEvent" -n src
grep -R "HoverEvent" -n src

6. Update the Gradle dependencies so RoseChat is compiled against the Adventure/Paper API used by Purpur 1.21.11.

7. Clean the old build:

./gradlew clean

8. Build RoseChat:

./gradlew build --no-daemon

9. Find the newly built JAR:

ls -lh build/libs/

10. Stop the Minecraft server.

11. Back up the existing RoseChat plugin:

mv plugins/RoseChat-RC-4.jar plugins/RoseChat-RC-4.jar.backup

12. Copy the newly built RoseChat JAR into plugins/.

13. Start the server.

14. Test chat.

15. If another NoClassDefFoundError appears, search the source for that missing Adventure class and migrate that API usage as well.

IMPORTANT:
Do NOT install a random Adventure JAR into the plugins folder.
Purpur already provides the Adventure API.

The goal is to make RoseChat compatible with the Adventure API used by Purpur 1.21.11, rather than forcing an older Adventure API onto the server.