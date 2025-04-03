# imad-Assignment1

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val inputTime = findViewById<EditText>(R.id.inputTime)
        val btnSuggest = findViewById<Button>(R.id.btnGetSuggestion)
        val btnReset = findViewById<Button>(R.id.btnReset)
        val btnNavigate = findViewById<Button>(R.id.btnNavigate)

        val mealSuggestions = mapOf(
            "morning" to "Eggs",
            "mid-morning" to "Fruit",
            "afternoon" to "Sandwich",
            "mid-afternoon" to "Cake",
            "dinner" to "Cake",
            "after dinner" to "Ice cream",
        )

        btnSuggest.setOnClickListener{
            val input = inputTime.text.toString().trim().lowercase()
            val validKey = mealSuggestions.keys.find{it.equals(input,ignoreCase = true)}
            val suggestion = if (validKey != null) {
                mealSuggestions[validKey]
            }else {
                "Invalid time of day. Enter Morning, Mid-Morning, Afternoon, Mid-afternoon, Dinner, or After dinner"
            }

            val intent = Intent(this,SecondActivity::class.java)
            intent.putExtra("meal_suggestion",suggestion)
            startActivity(intent)
            }
        btnReset.setOnClickListener{
            inputTime.text.clear()
        }

SECOND ACTIVITY

class SecondActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_second)

        val mealSuggestionText = findViewById<TextView>(R.id.mealSuggestionText)
        val suggestion = intent.getStringExtra("meal_suggestion")
        mealSuggestionText.text = suggestion ?: "No suggestion available"
