# CharlesCD Circle Matcher

![build](https://github.com/ZupIT/charlescd-circle-matcher/workflows/build/badge.svg)
[![Maintainability](https://api.codeclimate.com/v1/badges/f65771dc7079c8f968fb/maintainability)](https://codeclimate.com/github/ZupIT/charlescd-circle-matcher/maintainability)
[![Coverage](https://api.codeclimate.com/v1/badges/f65771dc7079c8f968fb/test_coverage)](https://codeclimate.com/github/ZupIT/charlescd-circle-matcher/test_coverage)
![GitHub](https://img.shields.io/github/license/ZupIT/charlescd-circle-matcher)

This repository is part of [CharlesCD](https://github.com/ZupIT/charlescd) project.

Circle Matcher is a HTTP service that allows us to identify which logical segmentation rules the application user (managed by CharlesCD) belongs to.

## How it works
With CharlesCD it is possible to deploy your application, defining which user segment (circle) it belongs to. Routing takes place at the service mesh level, so every request for the cluster - managed by CharlesCD - needs segment information (circle id) for it to work properly.

Circle Matcher is a service that receives a JSON (without a specific contract) with the user's attributes (
any attribute that matters) and returns the identifier of the circle to which it belongs.

See an sample request:

```
POST /identify HTTP/1.1
Host: YOUR_PUBLIC_CLUSTER_HOST
Content-Type: application/json
X-Application-Id: CHARLESCD_WORKSPACE_ID

{
	"age": "27",
	"children": "2",
	"gender": "female"
}

```

The response could be:

```
{
    "circles": [
        {
            "id": "3ab6ec63-6378-4deb-9c74-97294ed75bcb",
            "name": "Some Circle Name"
        }
    ]
}

```
Then, simply use the circle identification information for any service call in your cluster. To do this, use the HTTP header **X-Circle-Id** with the value of **circles.id**.

Installation instructions [here](https://docs.charlescd.io/usando-o-charles/instalacao-do-charles).

See the CharlesCD [documentation](https://docs.charlescd.io) for more information.

