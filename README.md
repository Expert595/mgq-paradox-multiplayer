MGQ PARADOX ONLINE CO-OP v0.1.27
=================================

DELAYED HOST BATTLE-RETURN TRANSFER FIX
---------------------------------------
v0.1.27 fixes the remaining case where P2 stayed independent immediately after
battle, but was pulled beside P1 later when the HOST opened/closed the menu.

ROOT CAUSE
----------
MGQ can leave a same-map transfer reserved after a random battle and delay its
actual perform_transfer until a later scene boundary. The Host menu/autosave is
one such boundary. Earlier builds used a short frame-based battle return guard,
so that delayed transfer could occur after the guard expired and then be sent to
P2 as if it were a real party transfer.

FIX
---
* Random Host battles now arm a one-shot same-map transfer quarantine.
* The quarantine survives menus and other UI scene changes.
* The stale post-battle transfer is swallowed locally whenever MGQ eventually
  performs it, even if that is much later.
* That transfer is not broadcast to P2.
* The Host's remote P2 avatar is not moved by the swallowed transfer.
* The quarantine clears when consumed, on a real map change, or once P1
  deliberately walks away from the battle-entry tile.
* Non-JOIN authoritative campaign snapshots now preserve P2's local
  Game_Player object as a general multiplayer invariant.
* Added explicit Coop.log messages for quarantine arm/suppress/consume events.

EXPECTED TEST
-------------
1. Put P1 and P2 far apart on the same map.
2. Let P1 trigger and finish a random battle.
3. Do not move P1 afterward.
4. Open and close P1's menu.
5. P2 must remain at P2's own position.
6. Coop.log should show the delayed transfer being suppressed/consumed if MGQ
   actually performs one at that scene boundary.
7. Repeat after P1 walks at least one tile. The quarantine should clear normally.

INSTALL
-------
1. CLOSE ALL MGQ Game.exe instances.
2. Run Install_Coop.bat from this folder, or:
     Install_Coop.bat "D:\Games\MGQPRPG 3"
3. Install v0.1.27 in BOTH host and guest copies.
4. Confirm MGQCoopBackground.dll is beside Game.exe.
5. Both clients must use protocol 27.

ROLLBACK
--------
Install_Coop.bat preserves the first pre-co-op Data\Scripts.rvdata2 as:
  Data\Scripts.pre-coop-backup.rvdata2
Run Uninstall_Coop.bat to restore it.
