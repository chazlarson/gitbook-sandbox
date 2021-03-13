_Note: The following instructions have been replaced with the `update_sections` command._

# Scenario 1

## 1. Retrieve Plex Library Section IDs

You are going to need to retrieve the section IDs for all these libraries you added (which may or may not be in order). 

To get the Section IDs, go [[here|Plex Library Section IDs]].

For our example, it would look like this:

```
 2018-12-04 05:21:39,590 -     INFO -      PLEX [140360038001904]: Using Plex Scanner
  4: Anime
  5: Foreign Films
  6: Movies for Kids
  1: Movies
  3: Movies 4K
  2: TV Shows
```

_Note: TV Shows has the section ID of 2 because it was added second, after Movies, during initial setup._

## 2. Update config


_Note: For Mediabox / Feederbox setup, the following steps will be done on the Mediabox._

1. Open the Plex Autoscan Config file in your favorite editor (e.g. nano).

    ```
    nano /opt/plex_autoscan/config/config.json
    ```

1. Scroll down to the `PLEX_SECTION_PATH_MAPPINGS` section.

    1. Under this section, you will need to add your section IDs and the library paths (as they appear in Plex).

       The format will look like:

       ```json
       "SECTION_NUMBER": [
           "/data/Movies/<folderpath>/"
       ],
       ```

       Note 1: Make sure the folder paths are within quotes (e.g. `"/Movies/"`) and there is a comma (`,`) after the close bracket (`]`) - all except the last one (see example below).

       Note 2: Since folders ARE case sensitive, make sure the folder path matches the same case as the folders you created in Google Drive (e.g. `"/Movies/Movies-4K/"` is NOT the same as `"/Movies/Movies4k/"`).

    1. After the changes, the section will now look similar to this:

       ```json
       "PLEX_SECTION_PATH_MAPPINGS": {
          "1": [
              "/data/Movies/Movies/"
          ],
          "2": [
              "/data/TV/"
          ],
          "3": [
              "/data/Movies/4K/"
          ],
          "3": [
              "/data/Movies/Foreign/"
          ],
          "4": [
              "/data/Movies/Hollywood/"
          ],
          "5": [
              "/Movies/Kids/"
          ],
          "6": [
              "/TV/"
          ],
          "7": [
              "/Music/"
          ]
       },
       ```

1. <kbd class="platform-all">Ctrl + X</kbd> <kbd class="platform-all">Y</kbd> <kbd class="platform-all">Enter</kbd> to save.


1. Restart Plex Autoscan: `sudo systemctl restart plex_autoscan`


_Note: Do not modify `SERVER_PATH_MAPPINGS` as this does not require any changes._

# Scenario 2

## 1. Retrieve Plex Library Section IDs

You are going to need to retrieve the section IDs for all these libraries you added (which may or may not be in order). 

To get the Section IDs, go [[here|Plex Library Section IDs]].

For our example, it would look like this:

```
 2018-12-04 05:21:39,590 -     INFO -      PLEX [140360038001904]: Using Plex Scanner
  4: Anime
  5: Foreign Films
  6: Movies for Kids
  1: Movies
  3: Movies 4K
  2: TV Shows
```

_Note: TV Shows has the section ID of 2 because it was added second, after Movies, during initial setup._

## 2. Update config

_Note: For Mediabox / Feederbox setup, this will be done on the Mediabox._

1. On the server's shell, run the following command:

    ```
    nano /opt/plex_autoscan/config/config.json
    ```

1. Scroll down to the `PLEX_SECTION_PATH_MAPPINGS` section.

   1. Under this section, you will need to add your section IDs and the library paths (as located within the `/Media` folder in Google Drive).


       The format will look like:

       ```json
       "SECTION_NUMBER": [
           "/<folder>/"
       ],
       ```

       Note 1: Make sure the folder paths are within quotes (e.g. `"/Movies-3D"`) and there is a comma (`,`) after the close bracket (`]`) - all except the last one (see example below).

       Note 2: Since folders are case sensitive, make sure the folder path matches the same case as the folders you created in Google Drive (e.g. `"/Movies-4K"` is not the same as `"/Movies-4k"`).

   1. After the changes, the section will now look similar to this:

       ```json
       "PLEX_SECTION_PATH_MAPPINGS": {
          "1": [
              "/Movies-3D/"
          ],
          "2": [
              "/Movies-4K/"
          ],
          "3": [
              "/Movies-Foreign/"
          ],
          "4": [
              "/Movies-Hollywood/"
          ],
          "5": [
              "/Movies-Kids/"
          ],
          "6": [
              "/TV/"
          ],
          "7": [
              "/Music/"
          ]
       },
       ```

1. <kbd class="platform-all">Ctrl + X</kbd> <kbd class="platform-all">Y</kbd> <kbd class="platform-all">Enter</kbd> to save.


1. Restart Plex Autoscan: `sudo systemctl restart plex_autoscan`


_Note: Do not modify `SERVER_PATH_MAPPINGS` as this does not require any changes._