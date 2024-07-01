package top.mbr_ecs;

import com.github.dockerjava.api.DockerClient;
import com.github.dockerjava.api.command.CreateServiceResponse;
import com.github.dockerjava.api.model.*;
import com.github.dockerjava.core.DockerClientBuilder;

import java.util.Arrays;
import java.util.List;

//TIP To <b>Run</b> code, press <shortcut actionId="Run"/> or
// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
public class Main {
    public static void main(String[] args) {

        try{
            DockerClient dockerClient
                    = DockerClientBuilder.getInstance("tcp://192.168.96.192:2375").build();
            List<SwarmNode> result = dockerClient.listSwarmNodesCmd().exec();
            System.out.println(result);
            Service service = dockerClient.inspectServiceCmd("zfxggeieayu9").exec();
            System.out.println(service.toString());
        }
        catch (Exception e){
            e.printStackTrace();
        }
        try{
            DockerClient dockerClient
                    = DockerClientBuilder.getInstance("tcp://192.168.96.191:2375").build();
            List<SwarmNode> result = dockerClient.listSwarmNodesCmd().exec();
            System.out.println(result);
            Service service = dockerClient.inspectServiceCmd("zfxggeieayu9").exec();
            System.out.println(service.toString());
        }
        catch (Exception e){
            e.printStackTrace();
        }


        DockerClient dockerClient
                = DockerClientBuilder.getInstance("tcp://192.168.96.191:2375").build();

        //dockerClient.removeServiceCmd("v6x7ag7rfr47bhl6hud8ecqhd").exec();

        TaskSpec taskSpec = new TaskSpec().withContainerSpec(
                new ContainerSpec().withImage("tomcat:latest"));

        ServiceModeConfig serviceModeConfig = new ServiceModeConfig().
                withReplicated(new ServiceReplicatedModeOptions().withReplicas(3));

        EndpointSpec endpointSpec = new EndpointSpec()
                .withPorts(Arrays.asList(
                        new PortConfig()
                                .withProtocol(PortConfigProtocol.TCP)
                                .withPublishedPort(8081) // 主机上的发布端口 80
                                .withTargetPort(8080), // 容器内的目标端口 80
                        new PortConfig()
                                .withProtocol(PortConfigProtocol.TCP)
                                .withPublishedPort(443) // 主机上的发布端口 443
                                .withTargetPort(443) // 容器内的目标端口 443
                ));

        CreateServiceResponse serviceResponse = dockerClient.createServiceCmd(new ServiceSpec()
                .withName("mytomcat") // 设置服务名称
                .withTaskTemplate(taskSpec)
                .withMode(serviceModeConfig)
                .withEndpointSpec(endpointSpec)
        ).exec();
        System.out.println("Service created with ID: " + serviceResponse.getId());
        Service service = dockerClient.inspectServiceCmd(serviceResponse.getId()).exec();
        System.out.println(service);





    }
}
