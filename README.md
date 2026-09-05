MGQ PARADOX ONLINE CO-OP v0.1.27
=================================

DELAYED HOST BATTLE-RETURN TRANSFER FIX
---------------------------------------
v0.1.27 fixes the remaining case where P2 stayed independent immediately after
battle, but was pulled beside P1 later when the HOST opened/closed the menu.

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
