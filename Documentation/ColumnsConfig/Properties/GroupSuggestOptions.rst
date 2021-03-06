suggestOptions
~~~~~~~~~~~~~~

:aspect:`Datatype`
    array

:aspect:`Scope`
    Display

:aspect:`Description`
    **Only with internal\_type='db'**

    Optional, additional suggest options used if the suggest wizard is not
    :ref:`hidden <columns-group-properties-hideSuggest>`.

    Suggestions can be configured differently for each table. Settings in "default" are applied to all tables.
    In the example below, there is a special setting for the "pages" table to search only standard pages.

    .. code-block:: php

        'related_records' => [
            'label' => 'Related records',
            'config' => [
                'type' => 'group',
                'internal_type' => 'db',
                'allowed' => 'pages, tt_content',
                'suggestOptions' => [
                    'default' => [
                        'searchWholePhrase' => 1
                    ],
                    'pages' => [
                        'searchCondition' => 'doktype = 1'
                    ]
                ]
            ]
        ],

    pidList (list of values)
      Limit the search to certain pages (and their sub pages). When pidList is empty all pages will be included in the
      search (as long as the be\_user is allowed to see them).

      **Example**

      .. code-block:: php

          'storage_pid' => [
              'config' => [
                  'suggestOptions' => [
                      'default' => [
                          'pidList' => '1,2,3,45',
                      ],
                  ],
              ],
          ],

    pidDepth (integer)
      Expand pidList by this number of levels. Has an effect only if pidList has a value.

      **Example**

      .. code-block:: php

          'storage_pid' => [
              'config' => [
                  'suggestOptions' => [
                      'default' => [
                          'pidList' => '6,7',
                          'pidDepth' => 4
                      ],
                  ],
              ],
          ],

    minimumCharacters (integer)
      Minimum number of characters needed to start the search. Works only in "default" configuration array.

    maxItemsInResultList (integer)
      Maximum number of results to display, default is :code:`10`.

    maxPathTitleLength (integer)
      Maximum number of characters to display when a path element is too long.

    searchWholePhrase (boolean)
      Whether to do a :code:`LIKE=%mystring%` (searchWholePhrase = 1) or a :code:`LIKE=mystring%`
      (to do a real find as you type), default is :code:`0`.

      **Example**

      .. code-block:: php

          'storage_pid' => [
              'config' => [
                  'suggestOptions' => [
                      'default' => [
                          'searchWholePhrase' => 1,
                      ],
                  ],
              ],
          ],

    searchCondition (string)
      Additional WHERE clause (not prepended with :code:`AND`).

      .. note::
          Basically identical to 'addWhere' - one will vanish sooner or later.

      **Example**

      .. code-block:: php

          'storage_pid' => [
              'config' => [
                  'suggestOptions' => [
                      // configures the suggest wizard for the field "storage_pid"
                      // in table "pages" to search only for pages with doktype=1
                      'pages' => [
                          'searchCondition' => 'doktype=1',
                      ],
                  ],
              ],
          ],

    additionalSearchFields (string)
      Comma-separated list of fields the suggest wizard should also search in. By default the wizard looks only
      in the fields listed in the "label" and "label_alt" properties.

    addWhere (string)
      Allows to define an additional where clause for the searchquery. It supplies a marker for ###THIS_UID###
      which is useful to exclude the current record.

      .. note::
          Basically identical to 'searchCondition' - one will vanish sooner or later.

    orderBy (string)
      Allows to add an `ORDER BY` part to the search query.

    cssClass (string)
      Add a CSS class to every list item of the result list.

    receiverClass (string)
      PHP class alternative receiver class, default is `TYPO3\\CMS\\Backend\\Form\\WizardSuggestWizardDefaultReceiver`.
      Can be used to implement an own search strategy.

    renderFunc (string)
      User function to manipulate the displayed records in the results.
