## How to read build.gradle file in another build.gradle file.

Example Reading version from build.gradle file.

def props = new Properties()
file("${projectDir}/src/main/java/anyextraPath/build.gradle").withInputStream { props.load(it) }
def version= props.getProperty("version")?.replace("\"","")
