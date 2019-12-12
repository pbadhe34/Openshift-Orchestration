OC users and access rights

several factors are combined to make the decision when OpenShift Container Platform evaluates authorizations.

In details, it evaluates the identity (who), the actions (what), and the binding (how roles are applied to users).

Identity
	

In the context of authorization, both the username and list of groups the user belongs to.

Action
	

The action being performed. In most cases, this consists of:
Project 	The project being accessed.
Verb 	Can be get, list, create, update, delete, deletecollection or watch.
Resource Name 	The API endpoint being accessed.

Bindings
	

The full list of bindings.

A standard user on OpenShift is a member of 3 groups by default:

system:authenticated
This is assigned to all users who are identifiable to the API. Everyone who is not system:anonymous(the user) is in this group.

system:authenticated:oauth
This is assigned to all users who have been identified using an oauth token issued by the embedded oauth server. This is not applied to service accounts (they use service account tokens), or certificate users.

system:unauthenticated
This is assigned to users who have not presented credentials. Invalid credentials are rejected with a 401 error, so this is specifically users who did not try to authenticate at all.

Let’s see what roles are applied to our users/groups looking at the default clusterolebinding for the group system:authenticated.
