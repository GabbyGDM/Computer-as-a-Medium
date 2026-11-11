# Week 11

### Group Name: [N/A] (Just me!)
### Group Members:  Gabrielle Goover

# Youtube/VideoLink:  https://youtu.be/0hFIqqgAWqg


# Modified Scripts (all made by me, Gabrielle Goover):

### DangerSpotTrap
using UnityEngine;

public class DangerSpotTrap : MonoBehaviour
{
    public Animator animator;
    public DartTrap dartTrap;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
    }
    // Update is called once per frame
    void Update()
    {

    }

    private void OnTriggerEnter2D(Collider2D other)
    {

        if (other.CompareTag("Player"))
        {
            animator.SetBool("dart", true);

        }
    }
    private void OnTriggerExit2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            dartTrap.hasHit = false;
            animator.SetBool("dart", false);

        }
    }
}

### DartTrap
using UnityEngine;

public class DartTrap : MonoBehaviour
{
    public PlayerHealth playerHealth;
    public bool hasHit = false;


    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {

    }
    // Update is called once per frame
    void Update()
    {

    }

    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player") && hasHit == false)
        {
            playerHealth.health -= 10;
            hasHit = true;
            
        }
    }
}

### Enemy Attack
using UnityEngine;

public class EnemyAttack : MonoBehaviour
{
    public PlayerHealth playerHealth;
    public Enemy enemyHealth;
    public bool hasHit = false;
   
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
    }
    // Update is called once per frame
    void Update()
    {
    }
    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player") && hasHit == false)
        {
            playerHealth.health -= 10;
            
        }


        if (enemyHealth.enemyHealth <= 0)
        {
            Destroy(gameObject);
        }
    }    
}

### Health Pack
using UnityEngine;

public class HealthPack : MonoBehaviour
{

    public PlayerHealth playerHealth;
    public GameObject pack;

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        
    }
    // Update is called once per frame
    void Update()
    {
        
    }

    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player") && playerHealth.health < 100)
        {
            playerHealth.health += 10;
            Destroy(gameObject);
        }
        
    }
   
}

### MovingSpikeTrap (TriggerSpot)
using UnityEngine;

public class MovingSpikeTrap : MonoBehaviour
{
    public Animator animator;
    public SpikeTrap spikeTrap;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
    }
    // Update is called once per frame
    void Update()
    {

    }

    private void OnTriggerEnter2D(Collider2D other)
    {

        if (other.CompareTag("Player"))
        {
            animator.SetBool("spike", true);

        }
    }
    private void OnTriggerExit2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            spikeTrap.hasHit = false;
            animator.SetBool("spike", false);

        }
    }
}

### SpikeTrap (Actual Spikes)
using UnityEngine;

public class SpikeTrap : MonoBehaviour
{
    public PlayerHealth playerHealth;
    public bool hasHit = false;


    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {

    }
    // Update is called once per frame
    void Update()
    {

    }

    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player") && hasHit == false)
        {
            playerHealth.health -= 10;
            hasHit = true;

        }
    }
}

### SwordMana
using UnityEngine;
using UnityEngine.InputSystem;

public class SwordMana : MonoBehaviour
{
    public Animator animator;
    public Enemy enemyHealth;
    public int mana = 10;

    public TMP_Text swordMana;

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        swordMana.text = "Sword: ";
    }
    // Update is called once per frame
    void Update()
    {
        swordMana.text = "Sword: ";

    Attack();
    }
    void Attack()
    {
        if (Keyboard.current.fKey.wasPressedThisFrame)
        {
            animator.SetBool("mana", true);
            //mana -= 10;

        }
        else
        {
            animator.SetBool("mana", false);
            
        
        }
    }
    
    /*private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Mana"))
        {
            mana = 10;
        }
    }*/
    
}