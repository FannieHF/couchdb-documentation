.. Licensed under the Apache License, Version 2.0 (the "License"); you may not
.. use this file except in compliance with the License. You may obtain a copy of
.. the License at
..
..   http://www.apache.org/licenses/LICENSE-2.0
..
.. Unless required by applicable law or agreed to in writing, software
.. distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
.. WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
.. License for the specific language governing permissions and limitations under
.. the License.

.. highlight:: ini

======================
HTTP Resource Handlers
======================

.. _config/httpd_global_handlers:

Global HTTP Handlers
====================

.. config:section:: httpd_global_handlers :: Global HTTP Handlers

    These HTTP resources are provided for CouchDB server root level.

    .. config:option:: /

        ::

            [httpd_global_handlers]
            / = {couch_httpd_misc_handlers, handle_welcome_req, <<"Welcome">>}

    .. config:option:: favicon.ico

        The favicon handler looks for `favicon.ico` file within specified
        directory::

            [httpd_global_handlers]
            favicon.ico = {couch_httpd_misc_handlers, handle_favicon_req, "/usr/share/couchdb/www"}

    .. config:option:: _active_tasks

        ::

            [httpd_global_handlers]
            _active_tasks = {couch_httpd_misc_handlers, handle_task_status_req}

    .. config:option:: _all_dbs

        Provides a list of all server's databases::

            [httpd_global_handlers]
            _all_dbs = {couch_httpd_misc_handlers, handle_all_dbs_req}

        .. note::
            Sometimes you don't want to disclose database names for everyone,
            but you also don't like/want/able to set up any proxies in front of
            CouchDB. Removing this handler disables ``_all_dbs`` resource and
            there will be no way to get list of available databases.

            The same also is true for other resource handlers.

    .. config:option:: _config

        Provides resource to work with CouchDB config
        :ref:`remotely <api/config>`. Any config changes that was made via HTTP
        API are applied automatically on fly and doesn't requires server
        instance to be restarted::

            [httpd_global_handlers]
            _config = {couch_httpd_misc_handlers, handle_config_req}

        .. config:option:: _oauth

        ::

            [httpd_global_handlers]
            _oauth = {couch_httpd_oauth, handle_oauth_req}

    .. config:option:: _replicate

        Provides an API to run
        :ref:`temporary replications <api/server/replicate>`::

            [httpd_global_handlers]
            _replicate = {couch_replicator_httpd, handle_req}

    .. config:option:: _restart

        ::

            [httpd_global_handlers]
            _restart = {couch_httpd_misc_handlers, handle_restart_req}

    .. config:option:: _session

        Provides a resource with information about the current user's session::

            [httpd_global_handlers]
            _session = {couch_httpd_auth, handle_session_req}

    .. config:option:: _stats

        ::

            [httpd_global_handlers]
            _stats = {couch_httpd_stats_handlers, handle_stats_req}

    .. config:option:: _utils

        The :ref:`_utils <api/server/utils>` handler serves `Fauxton`'s web
        administration page::

            [httpd_global_handlers]
            _utils = {couch_httpd_misc_handlers, handle_utils_dir_req, "/usr/share/couchdb/www"}

        In similar way, you may set up custom handler to let CouchDB serve any
        static files.

    .. config:option:: _uuids

        Provides a resource to get UUIDs generated by CouchDB::

            [httpd_global_handlers]
            _uuids = {couch_httpd_misc_handlers, handle_uuids_req}

        This is useful when your client environment isn't capable of providing
        truly random IDs (web browsers e.g.).

.. _config/httpd_db_handlers:

Database HTTP Handlers
======================

.. config:section:: httpd_db_handlers :: Database HTTP Handlers

    These HTTP resources are available on every CouchDB database.

    .. config:option:: _all_docs

        ::

            [httpd_db_handlers]
            _all_docs = {couch_mrview_http, handle_all_docs_req}

    .. config:option:: _local_docs

        ::

            [httpd_db_handlers]
            _local_docs = {couch_mrview_http, handle_local_docs_req}

    .. config:option:: _design_docs

        ::

            [httpd_db_handlers]
            _design_docs = {couch_mrview_http, handle_design_docs_req}

    .. config:option:: _changes

        ::

            [httpd_db_handlers]
            _changes = {couch_httpd_db, handle_changes_req}

    .. config:option:: _compact

        ::

            [httpd_db_handlers]
            _compact = {couch_httpd_db, handle_compact_req}

    .. config:option:: _design

        ::

            [httpd_db_handlers]
            _design = {couch_httpd_db, handle_design_req}

    .. config:option:: _view_cleanup

        ::

            [httpd_db_handlers]
            _view_cleanup = {couch_mrview_http, handle_cleanup_req}

.. _config/httpd_design_handlers:

Design Documents HTTP Handlers
==============================

.. config:section:: httpd_design_handlers :: Design Documents HTTP Handlers

These HTTP resources are provided for design documents.

    .. config:option:: _compact

        ::

            [httpd_design_handlers]
            _compact = {couch_mrview_http, handle_compact_req}

    .. config:option:: _info

        ::

            [httpd_design_handlers]
            _info = {couch_mrview_http, handle_info_req}

    .. config:option:: _list

        ::

            [httpd_design_handlers]
            _list = {couch_mrview_show, handle_view_list_req}

    .. config:option:: _rewrite

        ::

            [httpd_design_handlers]
            _rewrite = {couch_httpd_rewrite, handle_rewrite_req}

    .. config:option:: _show

        ::

            [httpd_design_handlers]
            _show = {couch_mrview_show, handle_doc_show_req}

    .. config:option:: _update

        ::

            [httpd_design_handlers]
            _update = {couch_mrview_show, handle_doc_update_req}

    .. config:option:: _view

        ::

            [httpd_design_handlers]
            _view = {couch_mrview_http, handle_view_req}
