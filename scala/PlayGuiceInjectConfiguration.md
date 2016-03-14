To stub the following with the configuration an application would normally get when running play.

```scala
class Config @Inject()(config: play.Configuration) {
  val tableName: String = getMandatoryProperty("tableName")

  def getMandatoryProperty(propertyName: String): String =
    Option(config.getString(propertyName))
      .getOrElse(throw new RuntimeException(s"Required property '$propertyName' not set"))  
}
```

Use:

```scala
import com.typesafe.config.ConfigFactory
import play.Configuration
import java.io.File


class ApplicationDatabase @Inject()(config: Config) {
  val tableName: String = config.tablaName
}

object Main {
  def main(args: Array[String]) {
    val applicationConfiguration = ConfigFactory.parseFile(new File("location/conf/application.conf"))
    val testConfiguration = new Configuration(applicationConfiguration)

    new ApplicationDatabase(testConfiguration)
  }
}
```
