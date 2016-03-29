# gradleLearn
gradle

一.build.gradle
apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'application'
1.dependencies{
  compile files('lib/**.jar')
  compile group('common-collections',name:'commons-collections',version:'3.1')
  compile fileTree(dir:'lib/metric',include:['*.jar']) //编译整个文件夹下面的所有jar包
}

2.定义task
task loadJar(type:Jar){
    manifest {
        attributes 'Implementation-Title': 'load',
                   'Main-Class': 'load'
    }
    baseName = 'load'
    from { configurations.compile.collect { it.isDirectory() ? it : zipTree(it) } }
    with jar
}
执行gradle loadJar。
就导出了一个可执行的jar文件
