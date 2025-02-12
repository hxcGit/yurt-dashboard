yurt-dashboard is the web console for OpenYurt Novice Trial Platform.

```
|- backend              // Golang backend
    |-- k8s_client      // backend lib for requesting k8s
    |-- proxy_server    // backend api service
|- config               // user controller setting files
|- doc
    |-- design          // project design doc
    |-- help            // how to use yurt-dashboard doc
|- frontend             // React frontend
    |-- public
    |-- src
|- scripts              // cluster setup scripts
```

## Get Started

> Note: Since yurt-dashboard is essentially a web interface of an customized OpenYurt cluster, you need some extra work to run this project locally.

1. Prepare local development environment
   1. Create an OpenYurt Cluster. (You can setup the OpenYurt cluster [manually](https://github.com/openyurtio/openyurt/blob/master/docs/tutorial/manually-setup.md), but we recommend to start OpenYurt by using the [yurtctl](https://github.com/openyurtio/openyurt/blob/master/docs/tutorial/yurtctl.md) CLI tool.)
      - OpenYurt version needs to be **0.6.0+**
   2. Install User Controller. (yurt-dashboard's user management module depends on this User Controller)
      1. install User CRD, `cd ./config && kubectl apply -f ./user_crd.yaml`
      2. install yurt-user-controller, `cd ./config && kubectl apply -f ./user_controller.yaml` (Note: the yurt-user-controller image is still in progress, will be updated at any time, mainly for the convenience of daily debugging.)
      3. you can run `cd ./config && kubectl apply -f user_test.yaml` to test if your user CRD has been set up properly
   3. install yurt-dashboard dependencies
      - [Golang](https://go.dev/)
      - [Node.js](https://nodejs.dev/)
2. Install
   1. Start the backend server
      - The backend server needs a `kubeconfig` with admin privileges of your cluster set up in the last step, you need to provide it as a file located at `./backend/config/kubeconfig.conf`.
      - Start the backend server with `cd ./backend/proxy_server && go run .`
   2. How to play with the frontend
      - modify the backend server address `baseURL` at `./frontend/src/config.js`
      - install frontend dependencies `cd ./frontend && npm install`
      - develop
        - if you want to modify frontend behavior (start a frontend dev server) `npm run start`
        - if you just want a web interface (don't need to debug frontend code), use
          `npm run build` to generate frontend files

> If you want to change the GitHub OAuth behavior, we recommend you to [set up your own OAuth App with your account](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app), and replace the configurations in both [backend](./backend/proxy_server/auth.go) and [frontend](./frontend/src/components/User/LoginForm.jsx).

## Documentation

- [x] [OpenYurt Experience Center overall introduction](https://openyurt.io/docs/next/installation/openyurt-experience-center/overview)
- [x] [How to create an account in the experience center and get an out-of-box OpenYurt cluster](https://openyurt.io/docs/next/installation/openyurt-experience-center/user)
- [x] [How to join an user's node to the cluster and quickly deploy an app with one click](https://openyurt.io/docs/next/installation/openyurt-experience-center/web_console)
- [x] [How to use `kubeconfig` to experience OpenYurt capabilities](https://openyurt.io/docs/next/installation/openyurt-experience-center/kubeconfig)

## Todo List

The features which will be added into the yurt-dashboard are outlined here. Welcome to claim any of these!

| Task                                                                                               | Description                                                                                    | Assigned to | Current Status | priority (1-3) |
| -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ----------- | -------------- | -------------- |
| [Node status monitor](https://github.com/openyurtio/yurt-dashboard/issues/4)                       | display mem/CPU status of the node in the web interface Node panel                             |             | not assigned   | 1              |
| [A better logging system](https://github.com/openyurtio/yurt-dashboard/issues/10)                  |                                                                                                | @luc99hen   | in progress    | 1              |
| [Delete & Create resource from web console](https://github.com/openyurtio/yurt-dashboard/issues/6) |                                                                                                |             | not assigned   | 2              |
| [GitHub OAuth login](https://github.com/openyurtio/yurt-dashboard/issues/7)                        |                                                                                                | @hxcGit     | in progress    | 2              |
| [User experience optimization](https://github.com/openyurtio/yurt-dashboard/issues/8)              | e.g. display information about how many users or nodes are active                              |             | not assigned   | 2              |
| [Lab page refactor](https://github.com/openyurtio/yurt-dashboard/issues/9)                         | organize this page with OpenYurt's feature, e.g. Node autonomy; nodepool and united deployment |             | not assigned   | 3              |

## Contribute

You can pick any unassigned task in which you are interested and find the corresponding issue in this repository to let us know your interests. After that, you can follow the instructions from `Get Started` section to set up your local development environment.

By the way, we highly recommend to read the [contributing guide](https://github.com/openyurtio/openyurt/blob/master/CONTRIBUTING.md) through before making contributions.

## Contact

You can directly create an issue here or find the developer in the following group:

- Mailing List: openyurt@googlegroups.com
- Slack: [channel](https://join.slack.com/t/openyurt/shared_invite/zt-iw2lvjzm-MxLcBHWm01y1t2fiTD15Gw)
- Dingtalk Group (钉钉讨论群)

<div align="left">
    <img src="https://github.com/openyurtio/openyurt/blob/master/docs/img/ding.jpg" width=25% title="dingtalk">
</div>
