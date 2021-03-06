---
swagger: "2.0"
x-collection-name: Dropbox
x-complete: 0
info:
  title: Dropbox Core Search for files and folders by name.
  description: |-
    Returns metadata for all files and folders whose filename contains the given search string as a substring.

    Searches are limited to the folder path and its sub-folder hierarchy provided in the call.

    **Note:** Recent changes may not immediately be reflected in search results due to a short delay in indexing.
  termsOfService: https://www.dropbox.com/developers/reference/tos
  contact:
    name: Dropbox
    url: https://www.dropbox.com/developers
  version: 1.0.0
host: api.dropbox.com
basePath: /1
schemes:
- http
produces:
- application/json
consumes:
- application/json
paths:
  /reports/get_storage:
    post:
      summary: Get Storage
      description: Get storage.
      operationId: postReportsGetStorage
      x-api-path-slug: reportsget-storage-post
      parameters:
      - in: query
        name: end_date
        description: optional ending date (exclusive)
      - in: query
        name: start_date
        description: optional starting date (inclusive)
      responses:
        200:
          description: OK
      tags:
      - Storage
  /files/{root}/{path}:
    get:
      summary: Downloads a file.
      description: |-
        Downloads a file.

        This method also supports [HTTP Range Retrieval Requests](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.35.2)
        to allow retrieving partial file contents.
      operationId: downloads-a-filethis-method-also-supports-http-range-retrieval-requestshttpwwww3orgprotocolsrfc2616r
      x-api-path-slug: filesrootpath-get
      parameters:
      - in: path
        name: path
        description: The path to the file you want to retrieve
      - in: query
        name: rev
        description: The revision of the file to retrieve
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Files
      - Root
      - Path
  /files_put/{root}/{path}:
    post:
      summary: Uploads a file using PUT semantics.
      description: |-
        Uploads a file using PUT semantics.

        The preferred HTTP method for this call is **PUT**. For compatibility with browser environments, the **POST**
        HTTP method is also recognized.

        **Note:** Providing a `Content-Length` header set to the size of the uploaded file is required so that the
        server can verify that it has received the entire file contents.

        **Note:** `/files_put` has a maximum file size limit of 150 MB and does not support uploads with chunked
        encoding. To upload larger files, use [/chunked_upload](https://www.dropbox.com/developers/core/docs#chunked-upload)
        instead.
      operationId: uploads-a-file-using-put-semanticsthe-preferred-http-method-for-this-call-is-put-for-compatibility-w
      x-api-path-slug: files-putrootpath-post
      parameters:
      - in: query
        name: autorename
        description: This value, either `true` (default) or `false`, determines what
          happens when there is a conflict
      - in: body
        name: file_content
        description: The file contents to be uploaded
        schema:
          $ref: '#/definitions/holder'
      - in: query
        name: locale
        description: The metadata returned on successful upload will have its `size`
          field translated based on the given locale
      - in: query
        name: overwrite
        description: This value, either `true` (default) or `false`, determines whether
          an existing file will be overwrittenby this upload
      - in: query
        name: parent_rev
        description: If present, this parameter specifies the revision of the file
          youre editing
      - in: path
        name: path
        description: The full path to the file you want to write to
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Files
      - Put
      - Root
      - Path
    put:
      summary: Uploads a file using PUT semantics.
      description: |-
        Uploads a file using PUT semantics.

        The preferred HTTP method for this call is **PUT**. For compatibility with browser environments, the **POST**
        HTTP method is also recognized.

        **Note:** Providing a `Content-Length` header set to the size of the uploaded file is required so that the
        server can verify that it has received the entire file contents.

        **Note:** `/files_put` has a maximum file size limit of 150 MB and does not support uploads with chunked
        encoding. To upload larger files, use [/chunked_upload](https://www.dropbox.com/developers/core/docs#chunked-upload)
        instead.
      operationId: uploads-a-file-using-put-semanticsthe-preferred-http-method-for-this-call-is-put-for-compatibility-w
      x-api-path-slug: files-putrootpath-put
      parameters:
      - in: query
        name: autorename
        description: This value, either `true` (default) or `false`, determines what
          happens when there is a conflict
      - in: body
        name: file_content
        description: The file contents to be uploaded
        schema:
          $ref: '#/definitions/holder'
      - in: query
        name: locale
        description: The metadata returned on successful upload will have its `size`
          field translated based on the given locale
      - in: query
        name: overwrite
        description: This value, either `true` (default) or `false`, determines whether
          an existing file will be overwrittenby this upload
      - in: query
        name: parent_rev
        description: If present, this parameter specifies the revision of the file
          youre editing
      - in: path
        name: path
        description: The full path to the file you want to write to
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Files
      - Put
      - Root
      - Path
  /thumbnails/{root}/{path}:
    get:
      summary: Gets a thumbnail for an image.
      description: |-
        Gets a thumbnail for an image.

        This method currently supports files with the following file extensions: .jpg, .jpeg, .png, .tiff, .tif, .gif, .bmp

        Photos that are larger than 20MB in size won't be converted to a thumbnail.
      operationId: gets-a-thumbnail-for-an-imagethis-method-currently-supports-files-with-the-following-file-extensions
      x-api-path-slug: thumbnailsrootpath-get
      parameters:
      - in: query
        name: format
        description: For images that are photos, `jpeg` (default) should be preferred,
          while `png` is better for screenshots and digital art
      - in: path
        name: path
        description: The path to the image file you want to thumbnail
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      - in: query
        name: size
        description: Default size is `s`
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Thumbnails
      - Root
      - Path
  /previews/{root}/{path}:
    get:
      summary: Gets a preview for a file.
      description: |-
        Gets a preview for a file.

        Previews are only generated for the files with the following extensions: .doc, .docx, .docm, .ppt, .pps,
        .ppsx, .ppsm, .pptx, .pptm, .xls, .xlsx, .xlsm, .rtf
      operationId: gets-a-preview-for-a-filepreviews-are-only-generated-for-the-files-with-the-following-extensions-doc
      x-api-path-slug: previewsrootpath-get
      parameters:
      - in: path
        name: path
        description: The absolute path to the file you want to preview
      - in: query
        name: rev
        description: The revision of the file to retrieve
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Previews
      - Root
      - Path
  /chunked_upload:
    put:
      summary: Uploads large files to Dropbox in multiple chunks.
      description: |-
        Uploads large files to Dropbox in multiple chunks. Also has the ability to resume if the upload is interrupted.
        This allows for uploads larger than the `/files_put` maximum of 150 MB.

        Typical usage:
          1. Send a PUT request to `/chunked_upload` with the first chunk of the file without setting `upload_id`, and
          receive an `upload_id` in return.
          2. Repeatedly `PUT` subsequent chunks using the `upload_id` to identify the upload in progress and an `offset`
          representing the number of bytes transferred so far.
          3. After each chunk has been uploaded, the server returns a new offset representing the total amount transferred.
          4. After the last chunk, `POST` to `/commit_chunked_upload` to complete the upload.

        Chunks can be any size up to 150 MB. A typical chunk is 4 MB. Using large chunks will mean fewer calls
        to `/chunked_upload` and faster overall throughput. However, whenever a transfer is interrupted, you will
        have to resume at the beginning of the last chunk, so it is often safer to use smaller chunks.

        If the offset you submit does not match the expected offset on the server, the server will ignore the request
        and respond with a 400 error that includes the current offset. To resume upload, seek to the correct offset
        (in bytes) within the file and then resume uploading from that point.

        A chunked upload can take a maximum of 48 hours before expiring.
      operationId: uploads-large-files-to-dropbox-in-multiple-chunks-also-has-the-ability-to-resume-if-the-upload-is-in
      x-api-path-slug: chunked-upload-put
      parameters:
      - in: body
        name: file_content
        description: A chunk of data from the file being uploaded
        schema:
          $ref: '#/definitions/holder'
      - in: query
        name: offset
        description: The byte offset of this chunk, relative to the beginning of the
          full file
      - in: query
        name: upload_id
        description: The unique ID of the in-progress upload on the server
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Chunked
      - Upload
  /commit_chunked_upload/{root}/{path}:
    post:
      summary: Completes an upload initiated by the chunked upload method.
      description: |-
        Completes an upload initiated by the `/chunked_upload` method. Saves a file uploaded via `/chunked_upload` to
        a user's Dropbox.

        `/commit_chunked_upload` is similar to `/files_put`. The main difference is that while `/files_put` takes the
        file contents in the request body, `/commit_chunked_upload` takes a parameter `upload_id`, which is obtained
        when the file contents are uploaded via `/chunked_upload`.
      operationId: completes-an-upload-initiated-by-the-chunked-upload-method-saves-a-file-uploaded-via-chunked-upload-
      x-api-path-slug: commit-chunked-uploadrootpath-post
      parameters:
      - in: query
        name: autorename
        description: This value, either `true` (default) or `false`, determines what
          happens when there is a conflict
      - in: query
        name: locale
        description: The metadata returned on successful upload will have its `size`
          field translated based on the given locale
      - in: query
        name: overwrite
        description: This value, either `true` (default) or `false`, determines whether
          an existing file will be overwritten bythis upload
      - in: query
        name: parent_rev
        description: If present, this parameter specifies the revision of the file
          youre editing
      - in: path
        name: path
        description: The full path to the file you want to write to
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      - in: query
        name: upload_id
        description: Used to identify the chunked upload session youd like to commit
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Commit
      - Chunked
      - Upload
      - Root
      - Path
  /oauth2/token_from_oauth1:
    post:
      summary: Convert OAuth 1 token to OAuth 2 token.
      description: |-
        This endpoint should be used by apps transitioning from OAuth 1 to OAuth 2. It will return an OAuth 2 token
        for the authenticated user.
      operationId: this-endpoint-should-be-used-by-apps-transitioning-from-oauth-1-to-oauth-2-it-will-return-an-oauth-2
      x-api-path-slug: oauth2token-from-oauth1-post
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Oauth2
      - Token_from_oauth1
  /disable_access_token:
    post:
      summary: Disables the access token.
      description: Disables the access token used to authenticate the call. This method
        works for OAuth 1 and OAuth 2 tokens.
      operationId: disables-the-access-token-used-to-authenticate-the-call-this-method-works-for-oauth-1-and-oauth-2-to
      x-api-path-slug: disable-access-token-post
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Disable_access_token
  /account/info:
    get:
      summary: Retrieves information about the user's account.
      description: Retrieves information about the user's account.
      operationId: retrieves-information-about-the-users-account
      x-api-path-slug: accountinfo-get
      parameters:
      - in: query
        name: locale
        description: Use to specify language settings for user error messages and
          other language specific text
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Account
      - Info
  /metadata/{root}/{path}:
    get:
      summary: Retrieves file and folder metadata.
      description: |-
        Retrieves file and folder metadata.

        **Note:** `modified`, `rev`, and `revision` aren't returned in the metadata for the root/top-level path.
      operationId: retrieves-file-and-folder-metadatanote-modified-rev-and-revision-arent-returned-in-the-metadata-for-
      x-api-path-slug: metadatarootpath-get
      parameters:
      - in: query
        name: file_limit
        description: Default is 10,000 (max is 25,000)
      - in: query
        name: hash
        description: Each call to `/metadata` on a folder will return a `hash` field,
          generated by hashing all of the metadatacontained in that response
      - in: query
        name: include_deleted
        description: Only applicable when `list` is set
      - in: query
        name: include_media_info
        description: If `true`, each file will include a `photo_info` dictionary for
          photos and a `video_info` dictionaryfor videos with additional media info
      - in: query
        name: include_membership
        description: If `true`, metadata for a shared folder will include a list of
          members and a list of groups
      - in: query
        name: list
        description: The strings `true` and `false` are valid values
      - in: query
        name: locale
        description: The metadata returned will have its `size` field translated based
          on the given `locale`
      - in: path
        name: path
        description: The path to the file or folder
      - in: query
        name: rev
        description: If you include a particular revision number, then only the metadata
          for that revision will be returned
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Metadata
      - Root
      - Path
  /delta:
    post:
      summary: A way of letting you keep up with changes to files and folders in a
        user's Dropbox.
      description: |-
        A way of letting you keep up with changes to files and folders in a user's Dropbox.

        You can periodically call `/delta` to get a list of "delta entries", which are instructions on how to
        update your local state to match the server's state.

        If you use the `path_prefix` parameter, you must continue to pass the correct prefix on subsequent calls
        using the returned cursor. You can switch the `path_prefix` on any existing cursor to a descendant of the
        existing `path_prefix` on subsequent calls to `/delta`. For example if your cursor has no `path_prefix`,
        you can switch to any `path_prefix`. If your cursor has a `path_prefix` of "/Photos", you can switch it
        to "/Photos/Vacaction".

        When `include_media_info` is specified, files will only appear in delta responses when the media info is
        ready. If you use the `include_media_info` parameter, you must continue to pass the same value on subsequent
        calls using the returned cursor.

        **Important:** Unfortunately it is not possible to model correct Dropbox response with Swagger specification,
        due to [nested array](https://github.com/swagger-api/swagger-spec/issues/40) usage in delta response.

        Successful result [will return](https://gist.github.com/ando-takahiro/5203137) an array of delta `entries`.
        Each delta entry is a 2-item list of one of the following forms:

          * `[, ]` - Indicates that there is a file/folder at the given path. You should add the entry
          to your local state. The metadata value is the same as what would be returned by the `/metadata` call, except
          folder metadata doesn't have `hash` or `contents` fields. To correctly process delta entries:
            * If the new entry includes parent folders that don't yet exist in your local state, create those parent
            folders in your local state.
            * If the new entry is a file, replace whatever your local state has at path with the new entry.
            * If the new entry is a folder, check what your local state has at ``. If it's a file, replace it
            with the new entry. If it's a folder, apply the new `` to the folder, but don't modify the
            folder's children. If your local state doesn't yet include this path, create it as a folder.
            * If the new entry is a folder with the `read-only` field set to `true`, apply the read-only permission
            recursively to all files within the shared folder.
          * `[, null]` - Indicates that there is no file/folder at the given path. To update your local state
          to match, anything at path and all its children should be deleted. Deleting a folder in your Dropbox will
          sometimes send down a single deleted entry for that folder, and sometimes separate entries for the folder
          and all child paths. If your local state doesn't have anything at path, ignore this entry.

        **Note:** Dropbox treats file names in a case-insensitive but case-preserving way. To facilitate this,
        the `` values above are lower-cased versions of the actual path. The last path component of the
        `` value will be case-preserved.
      operationId: a-way-of-letting-you-keep-up-with-changes-to-files-and-folders-in-a-users-dropboxyou-can-periodicall
      x-api-path-slug: delta-post
      parameters:
      - in: formData
        name: cursor
        description: A string that is used to keep track of your current state
      - in: formData
        name: include_media_info
        description: If `true`, each file will include a `photo_info` dictionary for
          photos and a `video_info` dictionary forvideos with additional media info
      - in: formData
        name: locale
        description: The metadata returned will have its `size` field translated based
          on the given `locale`
      - in: formData
        name: path_prefix
        description: If present, this parameter filters the response to only include
          entries at or under the specified path
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Delta
  /delta/latest_cursor:
    post:
      summary: A way to quickly get a cursor for the server's state, for use with
        /delta.
      description: |-
        A way to quickly get a cursor for the server's state, for use with `/delta`.

        Unlike `/delta`, `/delta/latest_cursor` does not return any entries, so your app will not know about any
        existing files or folders in the Dropbox account. For example, if your app processes future delta entries
        and sees that a folder was deleted, your app won't know what files were in that folder. Use this endpoint
        if your app only needs to know about new files and modifications and doesn't need to know about files that
        already exist in Dropbox.

        If you need to build local state to match the server state in Dropbox, you should instead use `/delta`.
      operationId: a-way-to-quickly-get-a-cursor-for-the-servers-state-for-use-with-deltaunlike-delta-deltalatest-curso
      x-api-path-slug: deltalatest-cursor-post
      parameters:
      - in: formData
        name: include_media_info
        description: If `true`, the returned cursor will be encoded with `include_media_info`
          set to `true` for usewith `/delta`
      - in: formData
        name: path_prefix
        description: If present, the returned cursor will be encoded with a `path_prefix`
          for the specified path for usewith `/delta`
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Delta
      - Latest_cursor
  /revisions/{root}/{path}:
    get:
      summary: Obtains metadata for all available revisions of a file, including the
        current revision.
      description: |-
        Obtains metadata for all available revisions of a file, including the current revision.

        Only revisions up to thirty days old are available (or more if the Dropbox user has
        [Extended Version History](https://www.dropbox.com/help/113)). You can use the revision number in conjunction
        with the `/restore` call to revert the file to its previous state.
      operationId: obtains-metadata-for-all-available-revisions-of-a-file-including-the-current-revisiononly-revisions-
      x-api-path-slug: revisionsrootpath-get
      parameters:
      - in: query
        name: locale
        description: The metadata returned will have its `size` field translated based
          on the given `locale`
      - in: path
        name: path
        description: The path to the file
      - in: query
        name: rev_limit
        description: Default is 10
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Revisions
      - Root
      - Path
  /restore/{root}/{path}:
    post:
      summary: Restores a file path to a previous revision.
      description: |-
        Restores a file path to a previous revision.

        Unlike downloading a file at a given revision and then re-uploading it, this call is atomic. It also saves
        a bunch of bandwidth.
      operationId: restores-a-file-path-to-a-previous-revisionunlike-downloading-a-file-at-a-given-revision-and-then-re
      x-api-path-slug: restorerootpath-post
      parameters:
      - in: formData
        name: locale
        description: The metadata returned will have its `size` field translated based
          on the given `locale`
      - in: path
        name: path
        description: The path to the file
      - in: formData
        name: rev
        description: The revision of the file to restore
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Restore
      - Root
      - Path
  /search/{root}/{path}:
    get:
      summary: Search for files and folders by name.
      description: |-
        Returns metadata for all files and folders whose filename contains the given search string as a substring.

        Searches are limited to the folder path and its sub-folder hierarchy provided in the call.

        **Note:** Recent changes may not immediately be reflected in search results due to a short delay in indexing.
      operationId: returns-metadata-for-all-files-and-folders-whose-filename-contains-the-given-search-string-as-a-subs
      x-api-path-slug: searchrootpath-get
      parameters:
      - in: query
        name: file_limit
        description: The maximum and default value is 1,000
      - in: query
        name: include_deleted
        description: If this parameter is set to `true`, then files and folders that
          have been deleted will also be includedin the search
      - in: query
        name: include_membership
        description: If `true`, metadata for a shared folder will include a list of
          members and a list of groups
      - in: query
        name: locale
        description: The metadata returned will have its `size` field translated based
          on the given `locale`
      - in: path
        name: path
        description: The path to the folder you want to search from
      - in: query
        name: query
        description: The search string
      - in: path
        name: root
        description: 'Root folder: `auto` - automatically determines the appropriate
          root folder using your apps permissionlevel (recommended); `sandbox` - the
          codename for app folder level; `dropbox` - full dropbox access'
      responses:
        200:
          description: OK
      tags:
      - Storage
      - Documents
      - Search
      - Root
      - Path
x-streamrank:
  polling_total_time_average: 0
  polling_size_download_average: 0
  streaming_total_time_average: 0
  streaming_size_download_average: 0
  change_yes: 0
  change_no: 0
  time_percentage: 0
  size_percentage: 0
  change_percentage: 0
  last_run: ""
  days_run: 0
  minute_run: 0
---