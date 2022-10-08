---
description: For if you are struggling to figure out how it works :)
---

# An Example Command

```java
@Command(value = "oneconfig", aliases = {"ocfg"})
public class OneConfigCommand {

    @Main(description = "Opens the OneConfig GUI")
    private void main() {
        GuiUtils.displayScreen(OneConfigGui.create());
    }

    @SubCommand(description = "Opens the OneConfig HUD configurator.", aliases = {"edithud"})
    private void hud() {
        GuiUtils.displayScreen(new HudGui());
    }

    @SubCommand(description = "Destroy the currently open OneConfig GUI.")
    private void destroy() {
        OneConfigGui.INSTANCE = null;
    }

    @SubCommandGroup(value = "Profile", aliases = {"profiles"})
    private static class Profile {
        @SubCommand(description = "View all profiles", aliases = {"view"})
        private void list() {
            StringBuilder builder = new StringBuilder()
                    .append(ChatColor.GOLD).append("Available profiles:");
            for (String profile : Profiles.getProfiles()) {
                builder.append("\n");
                if (OneConfigConfig.currentProfile.equals(profile)) builder.append(ChatColor.GREEN);
                else builder.append(ChatColor.RED);
                builder.append(profile);
            }
            UChat.chat(builder.toString());
        }

        @SubCommand(description = "Switch to a Profile", aliases = {"enable", "set", "load", "switch"})
        private void switchProfile(@Description("Profile Name") @Greedy String profile) {
            if (!Profiles.doesProfileExist(profile)) {
                UChat.chat(ChatColor.RED + "The Profile \"" + profile + "\" does not exist!");
            } else {
                Profiles.loadProfile(profile);
                UChat.chat(ChatColor.GREEN + "Switched to the \"" + profile + "\" Profile.");
            }
        }

        @SubCommand(description = "Create a new Profile", aliases = {"make"})
        private void create(@Description("Profile Name") @Greedy String profile) {
            if (Profiles.doesProfileExist(profile)) {
                UChat.chat(ChatColor.RED + "The Profile \"" + profile + "\" already exists!");
            } else {
                Profiles.createProfile(profile);
                if (Profiles.doesProfileExist(profile)) Profiles.loadProfile(profile);
                UChat.chat(ChatColor.GREEN + "Created the \"" + profile + "\" Profile.");
            }
        }

        @SubCommand(description = "Rename a Profile")
        private void rename(@Description("Old name") String profile, @Description("New name") @Greedy String newName) {
            if (!Profiles.doesProfileExist(profile)) {
                UChat.chat(ChatColor.RED + "The Profile \"" + profile + "\" does not exist!");
            } else {
                Profiles.renameProfile(profile, newName);
                UChat.chat(ChatColor.GREEN + "Renamed the \"" + profile + "\" Profile to \" " + newName + "\".");
            }
        }

        @SubCommand(description = "Delete a Profile", aliases = {"remove", "destroy"})
        private void delete(@Description("Profile name") @Greedy String profile) {
            if (!Profiles.doesProfileExist(profile)) {
                UChat.chat(ChatColor.RED + "The Profile \"" + profile + "\" does not exist!");
            } else {
                Profiles.deleteProfile(profile);
                UChat.chat(ChatColor.GREEN + "Deleted the \"" + profile + "\" Profile.");
            }
        }
    }
}
```
