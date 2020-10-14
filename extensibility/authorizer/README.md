### Authorizer

This samples show how to inject a low-level authorizer component that can control access to all API calls.

The sample implementation of an authorizer `myAuthorizer` allows all requests to the "temporal-system" namespace and denies `UpdateNameSpace` calls for all other namespaces.

### Steps to run this sample
1. Start dependencies with `make start-dependencies` executed from the main Temporal repository as described in the [contribution guide](https://github.com/temporalio/temporal/blob/master/CONTRIBUTING.md#runing-server-locally).

2. Create database schema with `make install-schema`.

3. Start Temporal with the sample by running `go run authorizer/server/main.go`.

4. Use `tctl` to interact with Temporal

- Run `tctl n l` to list available namespaces. You should only see "temporal-system" initially.
- Run `tctl --ns test n register to create a namespace "test"
- Run `tctl n l` To see "test" listed
- Run `tctl --ns test n update` to try to update the "test" namespace. You should see a `PermissionDenied` error because `myAuthorizer` denies `UpdateNameSpace` calls.
