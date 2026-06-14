``` kotlin

package com.example.dialogv1

import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.background
import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.material3.Card
import androidx.compose.material3.CardDefaults
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

// Добавил модель одного заказа
data class OrderItem(
    val orderNumber: String,
    val productName: String,
    val productDescription: String,
    val currentPrice: String,
    val oldPrice: String,
    val time: String
)

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()

        setContent {
            MaterialTheme {
                OrdersScreen()
            }
        }
    }

    @Preview(showSystemUi = true)
    @Composable
    fun OrdersScreen() {
        // Добавил список из трех элементов
        val orders = listOf(
            OrderItem(
                orderNumber = "№ 854632154",
                productName = "Nike Air Max 270",
                productDescription = "Essential",
                currentPrice = "$270.68",
                oldPrice = "$150.00",
                time = "7 мин назад"
            ),
            OrderItem(
                orderNumber = "№ 325556516",
                productName = "Nike Air Max 270",
                productDescription = "Essential",
                currentPrice = "$364.95",
                oldPrice = "$260.00",
                time = "10:23"
            ),
            OrderItem(
                orderNumber = "№ 215485412",
                productName = "Nike Air Max",
                productDescription = "Essential",
                currentPrice = "$378.76",
                oldPrice = "$268.00",
                time = "18:34"
            )
        )

        Column(
            modifier = Modifier
                .fillMaxSize()
                .background(Color.White)
                .padding(horizontal = 20.dp)
        ) {
            Spacer(modifier = Modifier.height(72.dp))

            // Добавил прокручиваемый список
            LazyColumn(
                modifier = Modifier.fillMaxSize()
            ) {
                items(orders) { order ->
                    OrderCard(order = order)

                    Spacer(modifier = Modifier.height(14.dp))
                }
            }
        }
    }

    @Composable
    fun OrderCard(order: OrderItem) {
        Card(
            modifier = Modifier
                .fillMaxWidth()
                .height(118.dp)
                .clickable {
                    // Добавил обработку короткого нажатия
                    Toast.makeText(
                        this@MainActivity,
                        order.orderNumber,
                        Toast.LENGTH_SHORT
                    ).show()
                },
            shape = RoundedCornerShape(10.dp),
            colors = CardDefaults.cardColors(
                containerColor = Color(0xFFF7F7F9)
            )
        ) {
            Row(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(horizontal = 12.dp, vertical = 10.dp),
                verticalAlignment = Alignment.CenterVertically
            ) {
                // Добавил изображение товара через простой символ
                Box(
                    modifier = Modifier
                        .size(width = 70.dp, height = 58.dp),
                    contentAlignment = Alignment.Center
                ) {
                    Text(
                        text = "👟",
                        fontSize = 40.sp
                    )
                }

                Column(
                    modifier = Modifier
                        .weight(1f)
                        .padding(start = 8.dp)
                ) {
                    Text(
                        text = order.orderNumber,
                        fontSize = 14.sp,
                        color = Color(0xFF20AEEB)
                    )

                    Spacer(modifier = Modifier.height(2.dp))

                    Text(
                        text = order.productName,
                        fontSize = 14.sp,
                        color = Color.Black
                    )

                    Spacer(modifier = Modifier.height(2.dp))

                    Text(
                        text = order.productDescription,
                        fontSize = 14.sp,
                        color = Color.Black
                    )

                    Spacer(modifier = Modifier.height(4.dp))

                    Row {
                        Text(
                            text = order.currentPrice,
                            fontSize = 14.sp,
                            fontWeight = FontWeight.Bold,
                            color = Color.Black
                        )

                        Text(
                            text = order.oldPrice,
                            fontSize = 14.sp,
                            color = Color(0xFF666666),
                            modifier = Modifier.padding(start = 16.dp)
                        )
                    }
                }

                Text(
                    text = order.time,
                    fontSize = 14.sp,
                    color = Color(0xFF666666),
                    modifier = Modifier
                        .align(Alignment.Top)
                        .padding(top = 8.dp)
                )
            }
        }
    }
}


'''
