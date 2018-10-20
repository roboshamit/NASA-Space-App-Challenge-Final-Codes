# NASA-Space-App-Challenge-Final-Codes

using System.Collections;
using System.Collections.Generic;
using UnityEngine;


public class Player : MonoBehaviour
{
    public float sidespeed = 15f;
    public float mapWidth = 5f;
    private Rigidbody2D rb;
    public GameObject bulletPrefab;
    public float dirx;
    public Animator anim;
    Animator animator;
    public string isleft;
    public string isright;
    private bool left, right;
    private AudioSource matdestroy;
    // Use this for initialization
    void Start()
    {
        
        //animator.SetBool("isleft", false);
        anim = GetComponent<Animator>();
        rb = GetComponent<Rigidbody2D>();
        matdestroy = GetComponent<AudioSource>();
    }

    // Update is called once per frame
    void FixedUpdate()
    {
        dirx = Input.acceleration.x * sidespeed; //android
        float x = Input.GetAxis("Horizontal") * Time.fixedDeltaTime * sidespeed;
        Vector2 newposition = rb.position + Vector2.right * x;
        newposition.x = Mathf.Clamp(newposition.x, -mapWidth, mapWidth);
        if (newposition.x<rb.position.x)
        {
            GetComponent<Animator>().SetTrigger("isleft");
          //  
           
        }
        else if (newposition.x >rb.position.x)
        {
            GetComponent<Animator>().SetTrigger("isright");

        }
        else
        {
            GetComponent<Animator>().ResetTrigger("isleft");
            GetComponent<Animator>().ResetTrigger("isright");
        }
        
        rb.MovePosition(newposition);
        //android 
        rb.velocity = new Vector2(dirx, 0);
        if (Input.GetKeyDown("f"))
        {
            spawnBullet();
        }

    }
    void OnCollisionEnter2D(Collision2D col)
    {
        if (col.gameObject.tag == "Meteor")
        {
            FindObjectOfType<gameManager>().decreaseLife();
            matdestroy.Play();
            FindObjectOfType<hurtFrame>().HurtIndicator();////red frame

            //Debug.Log("gogog");
        }

    }


    public void spawnBullet()
    {
        Instantiate(bulletPrefab,transform.position, Quaternion.identity);
    }

}
