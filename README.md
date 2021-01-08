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
```

-----------------------------------------------------
### Unity Periodic Function Example
-----------------------------------------------------
 public Rigidbody2D projectile;

    void Start()
    {
        InvokeRepeating("LaunchProjectile", 2.0f, 0.3f);
    }

    void LaunchProjectile()
    {
        Rigidbody2D instance = Instantiate(projectile);

        instance.velocity = Random.insideUnitSphere * 5;
    }
................................

-----------------------------------------------------
### Unity Event Systems
-----------------------------------------------------
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System;
using UnityEngine.Events;

public class MyEvents : MonoBehaviour
{
    //1  EVENT HANDLER
    public event EventHandler OnEventHandler;
    //2  EVENT HANDLER -- Args pass
    public event EventHandler<SpacePressedEventCount> OnEventHandlerWithArg;
    public class SpacePressedEventCount
    {
        public float count;
    }
    int count = 5;

    // 3 Delegate event
    public event MyDelegate EventOnMyDelegate;
    public delegate void MyDelegate(string name);
    // 4 Action
    public Action<bool , int > ActionName;
    //5 Unity Event
    public UnityEvent OnUnityEvent;

    private void Start()
    {
        OnUnityEvent.AddListener(UnityEventListener);
    }
    
    void Update()
    {
        if(Input.GetKeyDown(KeyCode.Space))
        {
            //1  EVENT HANDLER
            OnEventHandler?.Invoke(this, EventArgs.Empty);
            //2  EVENT HANDLER -- Args pass
            OnEventHandlerWithArg?.Invoke(this, new SpacePressedEventCount{count = count});
            // 3 Delegate event
            EventOnMyDelegate?.Invoke("Maruf");
            // 4 Action
            ActionName?.Invoke(true, 28);
            //5 Unity Event
            OnUnityEvent?.Invoke();
        }
    }

    // 5 Unity Event. This event listener will be fired using Listener
    public void UnityEventListener()
    {
        Debug.Log("Unity Event Fired from MyEvent Class");
    }

}

```
### Event Subscriber from Another Classs

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System;
using UnityEngine.Events;

public class MyEventSubscriber : MonoBehaviour
{

   
    MyEvents myEvents;
    void Start()
    {
        myEvents = GetComponent<MyEvents>();
        //1  EVENT HANDLER
        myEvents.OnEventHandler += MyEvents_OnEventHandler;
        // 2 EVENT HANDLER Args
        myEvents.OnEventHandlerWithArg += MyEvents_OnEventHandlerWithArg;
        // 3 Event on Delegate
        myEvents.EventOnMyDelegate += MyEvents_EventOnMyDelegate;
        // 4 Action
        myEvents.ActionName += NyEvent_ActionName;
       
    }
    // 5 Unity Event. This event listener will be connected from Inspector
    public void UnityEventListener()
    {
        Debug.Log("Unity Event Fired");
    }

    // 4 Action
    private void NyEvent_ActionName(bool isSelected, int age)
    {
        Debug.Log("This Selected: " + isSelected + "Age: " + age);
    }
    // 3 Event Delegate
    private void MyEvents_EventOnMyDelegate(string name)
    {
        print("Name is: " + name);
    }
    // 2 EVENT HANDLER Args
    private void MyEvents_OnEventHandlerWithArg(object sender, MyEvents.SpacePressedEventCount e)
    {
        //  throw new NotImplementedException();
        Debug.Log("MyEvents_OnEventHandlerWithArg : " + e.count);
    }
    //1  EVENT HANDLER
    private void MyEvents_OnEventHandler(object sender, EventArgs e)
    {
        Debug.Log("MyEvents_OnEventHandler");
    }
   

   

}


```


...................................................

# Click to any object change color
.....................................................
Get Mouse or Mobile Touch

```C#
 if(Input.touchCount > 0 && Input.touches[0].phase == TouchPhase.Began)
        {
            Ray ray = Camera.main.ScreenPointToRay(Input.touches[0].position);
            RaycastHit hit;
            if(Physics.Raycast(ray,out hit))
            {
                if(hit.collider != null)
                {
                    Color color = new Color(Random.Range(0.0f, 1.0f), Random.Range(0.0f, 1.0f), Random.Range(0.0f, 1.0f));
                    hit.collider.GetComponent<MeshRenderer>().material.color = color;
                }
            }
          
        }
#if UNITY_EDITOR

        if (Input.GetMouseButton(0))
        {
            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
            RaycastHit hit;
            if (Physics.Raycast(ray, out hit))
            {
                if (hit.collider != null)
                {
                    Color color = new Color(Random.Range(0.0f, 1.0f), Random.Range(0.0f, 1.0f), Random.Range(0.0f, 1.0f));
                    hit.collider.GetComponent<MeshRenderer>().material.color = color;
                }
            }

        }

#endif

```

