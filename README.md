## Finale View

![Untitled](https://github.com/muhammeddincmdx/Kt-13-GridApp/assets/54439858/7ded0afb-0343-4f1b-a8fc-3b6ff74ff910)

### strings.xml
````
<resources>
    <string name="app_name">Courses</string>
    <string name="architecture">Architecture</string>
    <string name="automotive">Automotive</string>
    <string name="biology">Biology</string>
    <string name="crafts">Crafts</string>
    <string name="business">Business</string>
    <string name="culinary">Culinary</string>
    <string name="design">Design</string>
    <string name="ecology">Ecology</string>
    <string name="engineering">Engineering</string>
    <string name="fashion">Fashion</string>
    <string name="finance">Finance</string>
    <string name="film">Film</string>
    <string name="gaming">Gaming</string>
    <string name="geology">Geology</string>
    <string name="drawing">Drawing</string>
    <string name="history">History</string>
    <string name="journalism">Journalism</string>
    <string name="law">Law</string>
    <string name="lifestyle">Lifestyle</string>
    <string name="music">Music</string>
    <string name="painting">Painting</string>
    <string name="photography">Photography</string>
    <string name="physics">physics</string>
    <string name="tech">Tech</string>

</resources>
````

### dimens.xml
````
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <dimen name="padding_medium">16dp</dimen>
    <dimen name="padding_small">8dp</dimen>
</resources>
````


### data>DataSource.kt
````
package com.example.gridapp.data

import com.example.gridapp.R
import com.example.gridapp.model.Topic


    object DataSource {
        val topics = listOf(
            Topic(R.string.architecture, 58, R.drawable.architecture),
            Topic(R.string.automotive, 30, R.drawable.automotive),
            Topic(R.string.biology, 90, R.drawable.biology),
            Topic(R.string.crafts, 121, R.drawable.crafts),
            Topic(R.string.business, 78, R.drawable.business),
            Topic(R.string.culinary, 118, R.drawable.culinary),
            Topic(R.string.design, 423, R.drawable.design),
            Topic(R.string.ecology, 28, R.drawable.ecology),
            Topic(R.string.engineering, 67, R.drawable.engineering),
            Topic(R.string.fashion, 92, R.drawable.fashion),
            Topic(R.string.finance, 100, R.drawable.finance),
            Topic(R.string.film, 165, R.drawable.film),
            Topic(R.string.gaming, 37, R.drawable.gaming),
            Topic(R.string.geology, 290, R.drawable.geology),
            Topic(R.string.drawing, 326, R.drawable.drawing),
            Topic(R.string.history, 189, R.drawable.history),
            Topic(R.string.journalism, 96, R.drawable.journalism),
            Topic(R.string.law, 58, R.drawable.law),
            Topic(R.string.lifestyle, 305, R.drawable.lifestyle),
            Topic(R.string.music, 212, R.drawable.music),
            Topic(R.string.painting, 172, R.drawable.painting),
            Topic(R.string.photography, 321, R.drawable.photography),
            Topic(R.string.physics, 41, R.drawable.physics),
            Topic(R.string.tech, 118, R.drawable.tech),
        )
    }

````

### model>Topic.kt
````
package com.example.gridapp.model

import androidx.annotation.DrawableRes
import androidx.annotation.StringRes


data class Topic(
    @StringRes val name: Int,
    val availableCourses: Int,
    @DrawableRes val imageRes: Int
)
````

### MainActivity.kt
````
package com.example.gridapp

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.aspectRatio
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.lazy.grid.GridCells
import androidx.compose.foundation.lazy.grid.LazyVerticalGrid
import androidx.compose.foundation.lazy.grid.items
import androidx.compose.material3.Card
import androidx.compose.material3.Icon
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.layout.ContentScale
import androidx.compose.ui.res.dimensionResource
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.res.stringResource
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import com.example.gridapp.data.DataSource
import com.example.gridapp.model.Topic
import com.example.gridapp.ui.theme.GridAppTheme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            GridAppTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    TopicGrid(
                        modifier = Modifier.padding(
                            start = dimensionResource(R.dimen.padding_small),
                            top = dimensionResource(R.dimen.padding_small),
                            end = dimensionResource(R.dimen.padding_small),
                        )
                    )
                }
            }
        }
    }
}




//2
@Composable
fun TopicGrid(modifier: Modifier = Modifier) {
    LazyVerticalGrid(
        columns = GridCells.Fixed(1),
        verticalArrangement = Arrangement.spacedBy(dimensionResource(R.dimen.padding_small)),
        horizontalArrangement = Arrangement.spacedBy(dimensionResource(R.dimen.padding_small)),
        modifier = modifier
    ) {
        items(DataSource.topics) { topic ->
            TopicCard(topic)
        }
    }
}





//1
@Composable
fun TopicCard(topic: Topic,modifier:Modifier = Modifier) {
    Card {
        Row {
            Box{
                Image(painter = painterResource(id = topic.imageRes),
                    contentDescription =null,
                    modifier = modifier
                        .size(width = 68.dp, height = 68.dp)
                        .aspectRatio(1f),
                    contentScale = ContentScale.Crop


                )
            }


            Column {
                Text(text = stringResource(id = topic.name),
                    style = MaterialTheme.typography.bodyMedium,
                    modifier = Modifier
                        .padding(
                            start= dimensionResource(id = R.dimen.padding_medium),
                            end = dimensionResource(id = R.dimen.padding_medium),
                            top = dimensionResource(id = R.dimen.padding_medium),
                            bottom = dimensionResource(id = R.dimen.padding_small)
                        )
                )
                Row(verticalAlignment = Alignment.CenterVertically) {
                    Icon(painter = painterResource(id = R.drawable.ic_grain),
                        contentDescription = null,
                        modifier = Modifier.padding(
                            start = dimensionResource(id = R.dimen.padding_medium)
                        )
                    )
                    Text(text = topic.availableCourses.toString(),
                        style = MaterialTheme.typography.labelMedium,
                        modifier = Modifier.padding(
                            start = dimensionResource(id = R.dimen.padding_small)
                        )
                    )
                }
            }
        }
    }
}

@Preview(showBackground = true, showSystemUi = true)
@Composable
fun GreetingPreview() {
    GridAppTheme {
        val topic = Topic(R.string.photography, 321, R.drawable.photography)
        Column(
            modifier = Modifier.fillMaxSize(),
            verticalArrangement = Arrangement.Center,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            TopicCard(topic = topic)
        }
    }
}
````
