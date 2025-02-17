# Sample private image scan

This example performs a scan against an image located in a private registry.

## <a id="define-resources"></a>Define the resources

Create `sample-private-image-scan.yaml`:

```yaml
---
apiVersion: scanning.apps.tanzu.vmware.com/v1beta1
kind: ImageScan
metadata:
  name: sample-private-image-scan
spec:
  registry:
    image: IMAGE_URL
  scanTemplate: private-image-scan-template
```

Where:

- `IMAGE_URL` is the url of an image in a private registry.

> **NOTE:** The private image scan assumes that the target image secret was configured during Tanzu Application Platform installation.

## <a id="set-up-watch"></a>(Optional) Set up a watch

Before deploying, set up a watch in another terminal to see things process:

```console
watch kubectl get scantemplates,scanpolicies,sourcescans,imagescans,pods,jobs
```

For more information, see [Observing and Troubleshooting](../observing.md).

## <a id="deploy-resources"></a>Deploy the resources

```console
kubectl apply -f sample-private-image-scan.yaml
```

## <a id="view-scan-results"></a>View the scan results

When the scan completes, run:

```console
kubectl describe imagescan sample-private-image-scan
```

Notice the `Status.Conditions` includes a `Reason: JobFinished` and `Message: The scan job finished`.

For more information, see [Viewing and Understanding Scan Status Conditions](../results.md).

## <a id="clean-up"></a>Clean up

```console
kubectl delete -f sample-private-image-scan.yaml
```

## <a id="view-vuln-reports"></a>View vulnerability reports

After completing the scans, [query the Supply Chain Security Tools - Store](../../cli-plugins/insight/query-data.md) to view your vulnerability results.
