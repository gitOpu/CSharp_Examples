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

* Camera follow to the player (camera code, attach player)
```C#
public class CameraFollowPlayer : MonoBehaviour
{
    public Transform playerTransform;
    private Vector3 deltaTransofrm;
    void Start()
    {
        deltaTransofrm = transform.position - playerTransform.position;
    }

    // Update is called once per frame
    void Update()
    {
        transform.position = playerTransform.position + deltaTransofrm;
    }
}
#
