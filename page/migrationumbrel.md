How to migrate from Core to Knots on Umbrel.
=============

This guide works for versions of umbrel above 1.0!

1. Install Bitcoin Knots if its not already done!
2. Right click on Bitcoin Knots and click on stop.
3. Do the same with Bitcoin Core (also stop all applications than depend on Bitcoin)

<img src="migration/1-migration.png" width="50%" height="50%" />

4. Now we need to open the terminal:

Go to settings, click on the open button on the advanced settings section:

<img src="migration/2-migration.png" width="50%" height="50%" />

Click on the open button of the terminal:

<img src="migration/3-migration.png" width="50%" height="50%" />

Finaly open the "umbrelOS" terminal:

<img src="migration/4-migration.png" width="50%" height="50%" />

5. Paste this command and press enter to move the Blockchain data from Bitcoin Core to Knots:

```bash
cd umbrel/app-data/ && sudo rm -rf bitcoin-knots/data/ && sudo mv bitcoin/data/ bitcoin-knots/ && sudo rm -f bitcoin-knots/data/app/bitcoin-config.json
```

6. you can now close the terminal and get back to the main view.
7. Start Bitcoin Knots and see if the chain is synced!
8. Swap all app that require Bitcoin to Bitcoin Knots.

<img src="migration/5-migration.png" width="50%" height="50%" />

<img src="migration/6-migration.png" width="50%" height="50%" />

9. You can now uninstall Bitcoin Core.

Done! You now have migrated to Bitcoin Knots.


Here is a video demonstrating how to move to bitcoin Knots without typing any commands:

<video width="640" height="360" controls>
  <source src="migration/Migrate-Blockchain.mp4" type="video/mp4">
</video>
