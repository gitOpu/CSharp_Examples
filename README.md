# CSharp_Examples
This repository contains c sharp unity simple examples to perform a specific task

* Roated anything towards mouse
```C#
Vector3 pos = Camera.main.WorldToScreenPoint(transform.position);
        Vector3 dir = Input.mousePosition - pos;
        float angle = Mathf.Atan2(dir.y, dir.x) * Mathf.Rad2Deg;
       transform.rotation =Quaternion.AngleAxis(angle, Vector3.forward);
```

* Vector3 is not a point its a magnitude with a director say velocity
