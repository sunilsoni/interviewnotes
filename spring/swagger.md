Swagger
=======
Swagger is the world's largest framework of API developer tools for the OpenAPI Specification (OAS), enabling development across the entire API lifecycle, from design and documentation, to testing and deployment.

This API tool allows for REST API documentation that stays closer to the code and evolves along with it. As an API framework, Swagger allows us to use annotations on the resource classes and its resource methods. Swagger has a lot to offer, and many features that are beyond the scope of this short brief.

The basic idea is to document the code with enough metadata in the form of annotations and then use build tools such as Maven to generate a JSON or YAML document that describes the API. This generated file (swagger.yaml) can then be used in other swagger tools to browse and explore the APIs. There's also support for bundling swagger-ui with the project.

The Swagger website allows for two approaches, 
- one called top down that allows for defining the details via a Swagger editor and then using code generation tools to create the code conforming to the specification. 
- The bottom up approach, on the other hand, is used to create a Swagger definition from an existing REST API. 

Swagger API
-----------

You can make use of Swagger annotations by adding the Maven dependency to it. This allows us to use metadata on the resource class and methods that are then used by the code generation tools to generate the Swagger format from it.
The Maven dependency is required:

```xml
<dependency>
    <groupId>io.swagger.core.v3</groupId>
    <artifactId>swagger-annotations</artifactId>
    <version>2.1.10</version>
</dependency>
```

Swagger annotations
-----------
Then the resource class can have annotations such as:

- `@Api`: To mark a resource as a Swagger resource
- `@ApiOperation`: Describes an operation or typically an HTTP method against a specific path
- `@ApiResponse`: To describe the response of a method
- `@ApiParam`: Additional metadata for operational parameters of a method

Maven plugin
-----------
A Maven plugin can be used to generate the swagger.yaml file based on the metadata placed on the code:
```xml
<build>
    ...
    <plugin>
        <groupId>com.github.kongchen</groupId>
        <artifactId>swagger-maven-plugin</artifactId>
        <version>3.1.5</version>
        <configuration>
            <apiSources>
                <apiSource>
                    <springmvc>false</springmvc>
                    <locations>org.jee8ng.users.boundary</locations>
                    <schemes>http</schemes>
                    <host>localhost:8081</host>
                    <basePath>/${project.build.finalName}/resources
                    </basePath>
                    <info>
                        <title>Users API</title>
                        <version>v1</version>
                        <description>Users rest endpoints</description>
                    </info>
                    <outputFormats>yaml</outputFormats>
                    <swaggerDirectory>${basedir}/src/main/webapp
                    </swaggerDirectory>
                </apiSource>
            </apiSources>
        </configuration>
        <executions>
            <execution>
                <phase>compile</phase>
                <goals>
                    <goal>generate</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
    ...
</build>
```

The swaggerDirectory is where the swagger.yaml file gets generated. This way, it's possible to use a combination of plugins and annotations to create the Swagger Spec format with the desired output, such as JSON, configured here. The plugin and API details can be explored further on the Swagger website and on the GitHub pages of the plugin.
















