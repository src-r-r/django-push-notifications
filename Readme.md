# Django Push Notifications

This package makes it easy to support Push notifications. It works together with third party services such as `ZeroPush`.

You can easily add permissions to push devices by chaining those devices to a notification setting. For registering a new push device you can add custom permissions.

## Configuration
__TODO__

## Usage

### Register a device
To register a new device you can use the `register_push_device` method in `services`:
```python
from push_notifications.services from register_push_device


token = "<The device token>"
register_push_device(user, token)
```

You can also pass notification permissions directly to the `register_push_device` method:
```python
register_push_device(user, token, ['likes', 'comments'])
```

### Add permissions
To add an notification permission to a push device you can use the `add_permission` method on the `device` object:
```python
device.add_permission('likes')
```

Or adding multiple permissions
```python
device.add_permissions(['likes', 'comments'])
```

You can also use the `add_notification_permissions` method in `services`:
```python
from push_notifications.services import add_notification_permission 

add_notification_permissions(device, ['likes', 'comments'])
```

Or
```python
add_notification_permission(device, 'likes')
add_notification_permission(device, 'comments')
```

### Remove permissions
To remove a notification permission you can use `remove_permission` method on the `device` object:
```python
device.remove_permission('likes')
```

Or removing multiple permissions
```python
device.remove_permissions(['likes', 'comments'])
```

### Send a notification
To send a notification to a certain permission group you can call `send_push_notification` in `services`:
```python
from push_notifications import send_push_notification
from datetime import timedelta

send_push_notification('likes', 'This is the message', sound="annoyingSound.mp3",
                                                       badge_number=1
                                                       info={
                                                        "extra": "payload",
                                                        "in": "notification"
                                                       },
                                                       expiry=timedelta(days=30))
```

#### Description
`send_push_notification(notify_type, message, **kwargs)

**kwargs**
- `sound`: The sound that has to be played when sending the notification
- `bade_number`: The badge_number that has to be displayed __(iOS Only)__
- `info`: Extra payload that comes along the notification
- `expiry`: The expiry of the notification __Accepts timedelta and datetime object__


