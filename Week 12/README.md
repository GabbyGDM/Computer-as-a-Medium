# Week 12

### Group Name: [N/A] (Just me!)
### Group Members:  Gabrielle Goover

# Youtube/VideoLink:  https://youtu.be/4lGXUn8omkU

## Modified Scripts (made by me, Gabrielle Goover):


### Player Attack
using System;
using UnityEngine;
using UnityEngine.InputSystem;

public class PlayerAttack : MonoBehaviour
{
    public Animator animator;

    public GameObject bulletPrefab;
    public Transform firePoint;
    
    public GameObject sword;
    public GameObject gun;

    public bool isGun = false;
    public bool isSword = true;

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
    }
    // Update is called once per frame
    void Update()
    {
        SwitchWeapon();
    }

    void SwitchWeapon()
    {
        if (Keyboard.current.digit2Key.wasPressedThisFrame)
        {
            sword.SetActive(false);
            gun.SetActive(true);
            isGun = true;
            isSword = false;
        }
        else if (Keyboard.current.digit1Key.wasPressedThisFrame)
        {
            gun.SetActive(false);
            sword.SetActive(true);
            isGun = false;
            isSword = true;
        }

        if(isGun == true && Keyboard.current.fKey.wasPressedThisFrame)
        {
            Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
        }
        else if(isSword == true && Keyboard.current.fKey.isPressed)
        {
            animator.SetBool("attack", true);
        }
        else
        {
            animator.SetBool("attack", false);
        }
    }
}


### Bullet
using UnityEngine;

public class Bullet : MonoBehaviour
{
    public float speed = 10f;
    public float destroyTime = 3f;
    public Rigidbody2D rb;

    public Enemy enemyHealth;

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        rb.linearVelocity = transform.up * speed;
        Destroy(gameObject, destroyTime);
    }

    // Update is called once per frame
    void Update()
    {

    }

}


### Player Movement
using UnityEngine;
using UnityEngine.InputSystem;

public class PlayerMovement : MonoBehaviour
{
    public float moveSpeed;
    private float speedX = 0f;
    private float speedY = 0f;
    public Rigidbody2D rb;

    public SpriteRenderer spriteRenderer;

    public Sprite bearup;
    public Sprite beardown;
    public Sprite bearleft;
    public Sprite bearright;

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        Movement();
    }

    void Movement()
    {
        // Horizontal Movement
        if (Keyboard.current.aKey.isPressed)
        {
            speedX = -moveSpeed;
            spriteRenderer.sprite = bearleft;
        }
        else if (Keyboard.current.dKey.isPressed)
        {
            speedX = moveSpeed;
            spriteRenderer.sprite = bearright;
        }

        else
        {
            speedX = 0;
        }
        // Vertical Movement
        if (Keyboard.current.wKey.isPressed)
        {
            speedY = moveSpeed;
            spriteRenderer.sprite = bearup;
        }
        else if (Keyboard.current.sKey.isPressed)
        {
            speedY = -moveSpeed;
            spriteRenderer.sprite = beardown;
        }
        else
        {
            speedY = 0;
        }
        rb.linearVelocity = new Vector2(speedX, speedY);
    }
}


### Sword Movement
using UnityEngine;
using UnityEngine.InputSystem;

public class SwordMovement : MonoBehaviour
{
    public SpriteRenderer spriteRenderer;

    //public Sprite swordup;
    //public Sprite sworddown;
    //public Sprite swordleft;
    //public Sprite swordright;

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        if (Keyboard.current.aKey.isPressed)
        {
            transform.eulerAngles = new Vector3(0f, 0f, 0f);
            transform.localScale = new Vector3(-1f, 1f, 1f);
        }
        else if (Keyboard.current.dKey.isPressed)
        {
            transform.eulerAngles = new Vector3(0f, 0f, 0f);
            transform.localScale = new Vector3(1f, 1f, 1f);
        }

        else if (Keyboard.current.wKey.isPressed)
        {
            transform.localScale = new Vector3(1f, 1f, 1f); 
            transform.eulerAngles = new Vector3(0f, 0f, 0f);
            transform.eulerAngles = new Vector3(0f, 0f, 90f);
        }
        else if (Keyboard.current.sKey.isPressed)
        {
            transform.localScale = new Vector3(1f, 1f, 1f); 
            transform.eulerAngles = new Vector3(0f, 0f, 0f);
            transform.eulerAngles = new Vector3(0f, 0f, -90f);
        }
    }
}


### Gun Movement
using UnityEngine;
using UnityEngine.InputSystem;

public class GunMovement : MonoBehaviour
{
    public SpriteRenderer spriteRenderer;

    public GameObject gunbase;

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {

    }

    // Update is called once per frame
    void Update()
    {
        if (Keyboard.current.aKey.isPressed)
        {
            gunbase.SetActive(true); 
            transform.eulerAngles = new Vector3(0f, 0f, 0f);
            transform.localScale = new Vector3(-1f, 1f, 1f);
        }
        else if (Keyboard.current.dKey.isPressed)
        {
            gunbase.SetActive(true);
            transform.eulerAngles = new Vector3(0f, 0f, 0f);
            transform.localScale = new Vector3(1f, 1f, 1f);
        }

        else if (Keyboard.current.wKey.isPressed)
        {
            gunbase.SetActive(false);
            transform.localScale = new Vector3(1f, 1f, 1f);
            transform.eulerAngles = new Vector3(0f, 0f, 0f);
            transform.eulerAngles = new Vector3(0f, 0f, 90f);
        }
        else if (Keyboard.current.sKey.isPressed)
        {
            gunbase.SetActive(false);
            transform.localScale = new Vector3(1f, 1f, 1f);
            transform.eulerAngles = new Vector3(0f, 0f, 0f);
            transform.eulerAngles = new Vector3(0f, 0f, -90f);
        }
    }
}

### Enemy
using UnityEngine;

public class Enemy : MonoBehaviour
{
    public int enemyHealth = 50;

    public bool hasHit = false;

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
    }
    // Update is called once per frame
    void Update()
    {
        Death();
    }
    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Sword"))
        {
            enemyHealth -= 10;
     
        }

        if (other.CompareTag("Bullet") && hasHit == true)
        {
            enemyHealth -= 10;

        }
    }


    void Death()
    {
        if (enemyHealth <= 0)
        {
            Destroy(gameObject);
        }
    }

}