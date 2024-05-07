# Expression tools
Expression tools are basic tools come with Galaxy but not available by default. We need to add them to the tools list by adding some 
XML code to tool_conf.xml file. 

## Why do we need them
We need the tools for ALPPACA pipeline to convert the output results (file) from "Find SNP Sites" to single input value (fconst) to IQTree.   

https://github.com/galaxyproject/galaxy/tree/release_21.09/tools/expression_tools 

We need to restart the galaxy for the tools to appear. 

```
/opt/galaxy/21.09/config/tool_conf.xml 
```

Below code was added to tool_conf.xml 
```
<section id="expression_tools" name="Expression Tools">
  <tool file="expression_tools/parse_values_from_file.xml"/>
</section>
```
