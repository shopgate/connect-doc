---
stoplight-id: wu00cjby6gs8v
---

# App Permissions Module

The App Permissions module checks and requests runtime permissions for native capabilities such as the camera, location, push notifications, and app tracking transparency.

```jsx
import { AppPermissions } from '@shopgate/native-modules';
```

## Example React component

```jsx
import { useEffect, useState } from 'react';
import { AppPermissions } from '@shopgate/native-modules';

export function CameraPermissionButton() {
  const [cameraStatus, setCameraStatus] = useState('unknown');

  useEffect(() => {
    const loadPermission = async () => {
      const { permissions } = await AppPermissions.getAppPermissions({
        permissionIds: ['camera'],
      });

      setCameraStatus(permissions[0]?.status ?? 'unknown');
    };

    loadPermission();
  }, []);

  const requestCameraPermission = async () => {
    const { permissions } = await AppPermissions.requestAppPermissions({
      permissions: [{ permissionId: 'camera' }],
    });

    setCameraStatus(permissions[0]?.status ?? 'unknown');
  };

  return (
    <div>
      <p>Camera permission: {cameraStatus}</p>
      <button type="button" onClick={requestCameraPermission}>
        Allow camera
      </button>
    </div>
  );
}
```

## getAppPermissions(params)

```js
const result = await AppPermissions.getAppPermissions({
  permissionIds: ['camera', 'location', 'push', 'appTrackingTransparency'],
});

```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `permissionIds` | `string[]` | no | Permission IDs to inspect. |

Returns `{ permissions: PermissionResult[] }`.

## requestAppPermissions(params)

```js
const requested = await AppPermissions.requestAppPermissions({
  permissions: [{ permissionId: 'camera' }],
});
```

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `permissions` | `PermissionRequest[]` | yes | Permissions to request. |

Permission statuses are `granted`, `notDetermined`, `denied`, `notSupported`, or `unknown`.
