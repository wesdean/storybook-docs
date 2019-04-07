# Story Book Roadmap

[Back to README](README.md)

## <a id="rest-api">REST API</a>

- <a id="user-auth">User auth system</a> (in progress)
  - users table should store user id, username, password, disabled flag, archived flag
- Implement file logger. 
- <a id="user-roles">Create role system</a>
  - Roles: superuser, owner, author, editor, contributor, proofreader, reader
- <a id="forking">Create forking system</a>
  - A fork should store parent fork, creator id, title, description, story text, published flag, created at
  - A story is a root fork. (parent fork is null)
  - Each fork of a fork is a path the reader can take in the story. 
  - Only text stories will be initially supported. 
  - Roles
    - role permissions should be inherited to forks. Ideally inheritance over copying permission but performance needs to be tested with deep branching of stories. 
    - **owner**: can create, edit, publish, unpublished, delete fork and descendants. can create branches. can add other roles at owner level and below. 
    - **author**: can create, edit, publish, unpublished fork and descendants. can delete descendants. can create branches. can add contributors. 
    - **editor**: can edit, publish, unpublished fork. 
    - **contributor**: can create branches. 
    - **proofreader**: can read published and unpublished stories. 
    - **reader**: can read published stories. 
- <a id="activity-logger">Implement activity logger</a>
  - log user activity to a coded database table. 
  - log table will store log code, user id, target id timestamp, log notes. 
  - Log ID labels:
    - user created
    - user disabled
    - user enabled
    - user archived
    - user unarchived
    - user authenticated
    - user role created
    - user role deleted
    - fork created
    - fork previewed (description only)
    - fork read (story text retrieved)
    - fork edited
    - fork published
    - fork unpublished
    - fork deleted

## <a id="user-interface">User Interface</a>

The UI will be a multi-application Angular app. 

<a id="ui-ood">**Order of development:**</a>

- <a id="ui-ood-web">Web UI</a>
  - Reader
  - Author
  - Admin
- <a id="ui-ood-mobile">Mobile UI</a>
  - Reader
  - Author
  - Admin

<a id="ui-apps">**UI apps / libraries:**</a>

- Common library
- Web UI
  - Admin - functions for superuser and owners. 
  - Author - functions for authors, editors, contributors, and proofreaders. 
  - Reader - functions for readers. 
- Mobile hybrid app - Cordova will be used for the mobile app, but I haven’t decided whether to use Ionic. 
  - Admin
  - Author
  - Reader

### <a id="ui-offline">Offline / collaborative editing</a>

- Users should be notified when their device is offline. (via a permenantly visible notification bar)
- Users should be notified when other users are editing same fork. 
- When an offline user submits a change, the fork should be checked for other edits. If other edits exist, user should be given the option to overwrite based on role. (ie. author can overwrite contributor, contributor cannot overwrite author)
- A real-time database, such as Firebase, should be used for collaborative editing. Persistent changes should be saved to backend database. 