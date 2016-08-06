# sonosdoorbell
Second phase of doorbell project - Playing doorbell through selected Sonos zones

Builds on soco project https://github.com/SoCo/SoCo project, by adding zone group status snapshotting and restoration to complement the soco shapshot/restore fucntions.

This project is specific to my needs but could be easily adapted. The use case is to pause selected zones which may be grouped in any number of combinations, play a doorbell sound through them and then restore not only the playing state (volume, track if coordinator, etc.) but also to regroup them as they were originally--all without interrupting whatever the other players are doing at the time. Of course, TTS and other alert use cases would have similar requirements.

This is my first programming project since Commodore BASIC, so feel free to give suggestions and improve the code. Speed especially could be improved.

Functionality:
- (soco) Snapshotting the player status of each zone
- Querying the intial group status of each zone
- Buidling a descriptor list to document and store that status
- Unjoing the doorbell zones from their initial groups as needed
- Joining the doorbell zones in a group and playing the doorbell sound
- Unjoining the doorbell group and (soco) restoring each zone player's status
- Parsing the group status descriptor list for each zone and rejoining each zone to initial group based on that status

There are six categories of initial zone group status documented in the list descriptors. They are shown is code comments. Based on the descriptors, each category is restored to initial groups (or not) in one of four different ways.

Background:

Compared to other implementations using snapshot and restore that I can find, the complications for my scenario are:

1. The doorbell should be played on selected zones only, e.g., not in rooms where children may be sleeping or on a Playbar that may be playing TV audio. For my scenario at least, the "doorbell zones" vs. "non-doorbell zones" are fixed and do not change. Party mode or playing on all zones regardless of group configuration are not options.


2. Prior to playing the doorbell, zones in the house initially may be grouped in any number of possible combinations, they may be grouped all together in party mode, or none may be grouped. Groups could be composed of all doorbell zones, all non-doorbell zones or mixed zones. Initial group coordinators could be either doorbell zones or non-doorbell zones.

3. Invisible zones like half of a stereo pair or a SUB which is slave to a Playbar should be ignored as far as group processing goes. (As is, the grouping Boolean value returned by snapshot includes invisible zones.)

4. Non-doorbell zones should not change state (stop playing, be ungrouped or whatever) when other zones play the doorbell sound.

5. Groups should be restored after the doorbell is played.
