
Storage
-------

In this part, we will discover how to store data in the platform storage and access them.

Personal repository
^^^^^^^^^^^^^^^^^^^

Every user of the platform has its own :ref:`repository` called with the username (e.g user Mario Rossi [username: mrossi] has a repository called mrossi).

This repository have been created automatically when the user has been registered on the T2 Cloud Platform. You can check the existence of your own repository on the Terradue portal personal profile by simply visiting the following url: https://store.terradue.com/mrossi.
You should see a simple (empty) HTML index.

.. note:: replace **mrossi** by your own username

If by any chance, the reponse is 404, this means your repository does not exist yet, please contact support@terradue.com.


Upload data
^^^^^^^^^^^

Deploying a file in a repository is done using a simple PUT to the final URL where the data must be located.

.. code-block:: console

    curl -u mrossi:ABcdEF -X PUT "https://store.terradue.com/mrossi/FDCI/2016/08/results/FDCI_2016_08_OBS.dat" -T Desktop/FDCI_2016_08_OBS.dat


Once the file correctly updloaded, you should receive a response like this:

.. code-block:: json

    {
      "uri": "https://store.terradue.com/mrossi/FDCI/2016/08/results/FDCI_2016_08_OBS.dat",
      "downloadUri": "https://store.terradue.com/mrossi/FDCI/2016/08/results/FDCI_2016_08_OBS.dat",
      "repo": "mrossi",
      "path": "/FDCI/2016/08/results/FDCI_2016_08_OBS.dat",
      "created": "2016-08-25T10:55:89.021Z",
      "createdBy": "mrossi",
      "size": "3675615",
      "mimeType": "application/octet",
      "checksums":
      {
              "md5" : "23285d1984632347b6ad60800a26531b",
              "sha1" : "1add322bfc564ef570e334517d60f69d941607d2"
          },
      "originalChecksums":{
              "md5" : "23285d1984632347b6ad60800a26531b",
              "sha1" : "1add322bfc564ef570e334517d60f69d941607d2"
          }
    }


.. note:: If the data you uploaded is intented to be indexed in the catalogue then. Please use always the returned value ``downloadUri`` in the :ref:`enclosure <datacreateentries>` link of the entry.




Delete Data
^^^^^^^^^^^

You delete a file or a directory using the DELETE http request

.. code-block:: console

    curl -u mrossi:ABcdEF -X DELETE "https://store.terradue.com/mrossi/FDCI/2016/08/results"


Share Data
^^^^^^^^^^

.. note:: coming soon





