# Headline

> An awesome project.

## Activiti BPM Diagram
```
<?xml version="1.0" encoding="UTF-8"?>
<definitions xmlns="http://www.omg.org/spec/BPMN/20100524/MODEL" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:activiti="http://activiti.org/bpmn" xmlns:bpmndi="http://www.omg.org/spec/BPMN/20100524/DI" xmlns:omgdc="http://www.omg.org/spec/DD/20100524/DC" xmlns:omgdi="http://www.omg.org/spec/DD/20100524/DI" typeLanguage="http://www.w3.org/2001/XMLSchema" expressionLanguage="http://www.w3.org/1999/XPath" targetNamespace="http://www.activiti.org/test">
  <message id="msgNewBorrowOrder" name="NewBorrowOrder"></message>
  <message id="msgApprove" name="Approve"></message>
  <message id="msgRollback" name="Rollback"></message>
  <message id="msgPublish" name="Publish"></message>
  <message id="msgCancel" name="Cancel"></message>
  <message id="msgUnpublish" name="Unpublish"></message>
  <message id="msgMatch" name="Match"></message>
  <message id="msgClose" name="Close"></message>
  <message id="msgUnmatch" name="Unmatch"></message>
  <message id="msgInvest" name="Invest"></message>
  <process id="BorrowOrderProcess" name="Borrow Order Process" isExecutable="true">
    <eventBasedGateway id="eventgateway1" name="Event Gateway"></eventBasedGateway>
    <sequenceFlow id="flow4" sourceRef="eventgateway1" targetRef="msgEventApprove"></sequenceFlow>
    <eventBasedGateway id="eventgateway2" name="Parallel Gateway"></eventBasedGateway>
    <intermediateCatchEvent id="messageintermediatecatchevent2" name="MessageCatchEvent">
      <messageEventDefinition messageRef="msgPublish"></messageEventDefinition>
    </intermediateCatchEvent>
    <sequenceFlow id="flow7" sourceRef="eventgateway2" targetRef="messageintermediatecatchevent2"></sequenceFlow>
    <serviceTask id="servicetask3" name="Published" activiti:class="com.oriente.cashalo.backend.volt.delegates.BorrowOrderProcess.PublishedDelegate"></serviceTask>
    <sequenceFlow id="flow8" sourceRef="messageintermediatecatchevent2" targetRef="servicetask3"></sequenceFlow>
    <sequenceFlow id="flow9" sourceRef="servicetask15" targetRef="eventgateway3"></sequenceFlow>
    <eventBasedGateway id="eventgateway3" name="Exclusive Gateway"></eventBasedGateway>
    <intermediateCatchEvent id="messageintermediatecatchevent3" name="MessageCatchEvent">
      <messageEventDefinition messageRef="msgInvest"></messageEventDefinition>
    </intermediateCatchEvent>
    <sequenceFlow id="flow10" sourceRef="eventgateway3" targetRef="messageintermediatecatchevent3"></sequenceFlow>
    <serviceTask id="servicetask4" name="Invested" activiti:class="com.oriente.cashalo.backend.volt.delegates.BorrowOrderProcess.InvestedDelegate"></serviceTask>
    <sequenceFlow id="flow11" sourceRef="messageintermediatecatchevent3" targetRef="servicetask4"></sequenceFlow>
    <endEvent id="endevent1" name="End"></endEvent>
    <startEvent id="msgStartEvent" name="Message start">
      <messageEventDefinition messageRef="msgNewBorrowOrder"></messageEventDefinition>
    </startEvent>
    <intermediateCatchEvent id="msgEventApprove" name="Approve">
      <messageEventDefinition messageRef="msgApprove"></messageEventDefinition>
    </intermediateCatchEvent>
    <sequenceFlow id="flow6" sourceRef="msgEventApprove" targetRef="servicetask2"></sequenceFlow>
    <serviceTask id="servicetask2" name="Approved" activiti:class="com.oriente.cashalo.backend.volt.delegates.BorrowOrderProcess.ApprovedDelegate"></serviceTask>
    <sequenceFlow id="flow5" sourceRef="servicetask2" targetRef="eventgateway2"></sequenceFlow>
    <intermediateCatchEvent id="messageintermediatecatchevent11" name="Cancel">
      <messageEventDefinition messageRef="msgCancel"></messageEventDefinition>
    </intermediateCatchEvent>
    <sequenceFlow id="flow47" sourceRef="eventgateway1" targetRef="messageintermediatecatchevent11"></sequenceFlow>
    <sequenceFlow id="flow48" sourceRef="eventgateway2" targetRef="messageintermediatecatchevent11"></sequenceFlow>
    <serviceTask id="servicetask11" name="Cancelled" activiti:class="com.oriente.cashalo.backend.volt.delegates.BorrowOrderProcess.CancelledDelegate"></serviceTask>
    <sequenceFlow id="flow50" sourceRef="messageintermediatecatchevent11" targetRef="servicetask11"></sequenceFlow>
    <sequenceFlow id="flow51" sourceRef="servicetask11" targetRef="eventgateway6"></sequenceFlow>
    <eventBasedGateway id="eventgateway6" name="Exclusive Gateway"></eventBasedGateway>
    <intermediateCatchEvent id="messageintermediatecatchevent12" name="MessageCatchEvent">
      <messageEventDefinition messageRef="msgClose"></messageEventDefinition>
    </intermediateCatchEvent>
    <sequenceFlow id="flow52" sourceRef="eventgateway6" targetRef="messageintermediatecatchevent12"></sequenceFlow>
    <serviceTask id="servicetask12" name="Closed" activiti:class="com.oriente.cashalo.backend.volt.delegates.BorrowOrderProcess.ClosedDelegate"></serviceTask>
    <sequenceFlow id="flow53" sourceRef="messageintermediatecatchevent12" targetRef="servicetask12"></sequenceFlow>
    <endEvent id="endevent3" name="End"></endEvent>
    <sequenceFlow id="flow54" sourceRef="servicetask12" targetRef="endevent3"></sequenceFlow>
    <serviceTask id="servicetask13" name="Submitted" activiti:class="com.oriente.cashalo.backend.volt.delegates.BorrowOrderProcess.SubmittedDelegate"></serviceTask>
    <sequenceFlow id="flow56" sourceRef="msgStartEvent" targetRef="servicetask13"></sequenceFlow>
    <sequenceFlow id="flow57" sourceRef="servicetask13" targetRef="eventgateway1"></sequenceFlow>
    <intermediateCatchEvent id="messageintermediatecatchevent14" name="Rollback">
      <messageEventDefinition messageRef="msgRollback"></messageEventDefinition>
    </intermediateCatchEvent>
    <sequenceFlow id="flow59" sourceRef="eventgateway2" targetRef="messageintermediatecatchevent14"></sequenceFlow>
    <sequenceFlow id="flow60" sourceRef="messageintermediatecatchevent14" targetRef="servicetask13"></sequenceFlow>
    <sequenceFlow id="flow61" sourceRef="eventgateway3" targetRef="messageintermediatecatchevent14"></sequenceFlow>
    <sequenceFlow id="flow63" sourceRef="servicetask3" targetRef="eventgateway7"></sequenceFlow>
    <eventBasedGateway id="eventgateway7" name="Exclusive Gateway"></eventBasedGateway>
    <intermediateCatchEvent id="messageintermediatecatchevent15" name="MessageCatchEvent">
      <messageEventDefinition messageRef="msgMatch"></messageEventDefinition>
    </intermediateCatchEvent>
    <sequenceFlow id="flow64" sourceRef="eventgateway7" targetRef="messageintermediatecatchevent15"></sequenceFlow>
    <serviceTask id="servicetask15" name="Matched" activiti:class="com.oriente.cashalo.backend.volt.delegates.BorrowOrderProcess.MatchedDelegate"></serviceTask>
    <sequenceFlow id="flow67" sourceRef="messageintermediatecatchevent15" targetRef="servicetask15"></sequenceFlow>
    <intermediateCatchEvent id="messageintermediatecatchevent16" name="MessageCatchEvent">
      <messageEventDefinition messageRef="msgUnpublish"></messageEventDefinition>
    </intermediateCatchEvent>
    <sequenceFlow id="flow70" sourceRef="eventgateway7" targetRef="messageintermediatecatchevent16"></sequenceFlow>
    <sequenceFlow id="flow71" sourceRef="messageintermediatecatchevent16" targetRef="servicetask2"></sequenceFlow>
    <intermediateCatchEvent id="messageintermediatecatchevent17" name="MessageCatchEvent">
      <messageEventDefinition messageRef="msgUnmatch"></messageEventDefinition>
    </intermediateCatchEvent>
    <sequenceFlow id="flow72" sourceRef="eventgateway3" targetRef="messageintermediatecatchevent17"></sequenceFlow>
    <sequenceFlow id="flow73" sourceRef="messageintermediatecatchevent17" targetRef="servicetask3"></sequenceFlow>
    <sequenceFlow id="flow74" sourceRef="servicetask4" targetRef="endevent1"></sequenceFlow>
    <sequenceFlow id="flow75" sourceRef="eventgateway6" targetRef="messageintermediatecatchevent14"></sequenceFlow>
    <textAnnotation id="textannotation1">
      <text>LendOrder Lent-out Succeed</text>
    </textAnnotation>
    <association id="association1" sourceRef="textannotation1" targetRef="messageintermediatecatchevent3"></association>
    <textAnnotation id="textannotation2">
      <text>InvestOrder Created</text>
    </textAnnotation>
    <association id="association2" sourceRef="textannotation2" targetRef="messageintermediatecatchevent15"></association>
    <textAnnotation id="textannotation3">
      <text>InvestOrder Cancelled</text>
    </textAnnotation>
    <association id="association3" sourceRef="textannotation3" targetRef="messageintermediatecatchevent17"></association>
  </process>
  <bpmndi:BPMNDiagram id="BPMNDiagram_BorrowOrderProcess">
    <bpmndi:BPMNPlane bpmnElement="BorrowOrderProcess" id="BPMNPlane_BorrowOrderProcess">
      <bpmndi:BPMNShape bpmnElement="eventgateway1" id="BPMNShape_eventgateway1">
        <omgdc:Bounds height="40.0" width="40.0" x="230.0" y="107.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="eventgateway2" id="BPMNShape_eventgateway2">
        <omgdc:Bounds height="40.0" width="40.0" x="549.0" y="107.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="messageintermediatecatchevent2" id="BPMNShape_messageintermediatecatchevent2">
        <omgdc:Bounds height="35.0" width="35.0" x="640.0" y="111.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="servicetask3" id="BPMNShape_servicetask3">
        <omgdc:Bounds height="55.0" width="136.0" x="700.0" y="100.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="eventgateway3" id="BPMNShape_eventgateway3">
        <omgdc:Bounds height="40.0" width="40.0" x="1184.0" y="108.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="messageintermediatecatchevent3" id="BPMNShape_messageintermediatecatchevent3">
        <omgdc:Bounds height="35.0" width="35.0" x="1269.0" y="111.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="servicetask4" id="BPMNShape_servicetask4">
        <omgdc:Bounds height="55.0" width="141.0" x="1330.0" y="102.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="endevent1" id="BPMNShape_endevent1">
        <omgdc:Bounds height="35.0" width="35.0" x="1490.0" y="112.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="msgStartEvent" id="BPMNShape_msgStartEvent">
        <omgdc:Bounds height="35.0" width="35.0" x="10.0" y="111.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="msgEventApprove" id="BPMNShape_msgEventApprove">
        <omgdc:Bounds height="35.0" width="35.0" x="320.0" y="110.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="servicetask2" id="BPMNShape_servicetask2">
        <omgdc:Bounds height="55.0" width="105.0" x="400.0" y="101.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="messageintermediatecatchevent11" id="BPMNShape_messageintermediatecatchevent11">
        <omgdc:Bounds height="35.0" width="35.0" x="640.0" y="370.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="servicetask11" id="BPMNShape_servicetask11">
        <omgdc:Bounds height="55.0" width="105.0" x="700.0" y="360.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="eventgateway6" id="BPMNShape_eventgateway6">
        <omgdc:Bounds height="40.0" width="40.0" x="850.0" y="368.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="messageintermediatecatchevent12" id="BPMNShape_messageintermediatecatchevent12">
        <omgdc:Bounds height="35.0" width="35.0" x="935.0" y="371.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="servicetask12" id="BPMNShape_servicetask12">
        <omgdc:Bounds height="55.0" width="105.0" x="1015.0" y="361.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="endevent3" id="BPMNShape_endevent3">
        <omgdc:Bounds height="35.0" width="35.0" x="1269.0" y="370.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="servicetask13" id="BPMNShape_servicetask13">
        <omgdc:Bounds height="55.0" width="105.0" x="90.0" y="101.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="messageintermediatecatchevent14" id="BPMNShape_messageintermediatecatchevent14">
        <omgdc:Bounds height="35.0" width="35.0" x="320.0" y="301.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="eventgateway7" id="BPMNShape_eventgateway7">
        <omgdc:Bounds height="40.0" width="40.0" x="881.0" y="108.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="messageintermediatecatchevent15" id="BPMNShape_messageintermediatecatchevent15">
        <omgdc:Bounds height="35.0" width="35.0" x="966.0" y="111.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="servicetask15" id="BPMNShape_servicetask15">
        <omgdc:Bounds height="55.0" width="105.0" x="1046.0" y="101.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="messageintermediatecatchevent16" id="BPMNShape_messageintermediatecatchevent16">
        <omgdc:Bounds height="35.0" width="35.0" x="966.0" y="43.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="messageintermediatecatchevent17" id="BPMNShape_messageintermediatecatchevent17">
        <omgdc:Bounds height="35.0" width="35.0" x="1269.0" y="184.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="textannotation1" id="BPMNShape_textannotation1">
        <omgdc:Bounds height="50.0" width="193.0" x="1223.0" y="21.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="textannotation2" id="BPMNShape_textannotation2">
        <omgdc:Bounds height="50.0" width="100.0" x="953.0" y="231.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape bpmnElement="textannotation3" id="BPMNShape_textannotation3">
        <omgdc:Bounds height="50.0" width="100.0" x="1270.0" y="241.0"></omgdc:Bounds>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNEdge bpmnElement="flow4" id="BPMNEdge_flow4">
        <omgdi:waypoint x="270.0" y="127.0"></omgdi:waypoint>
        <omgdi:waypoint x="320.0" y="127.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow7" id="BPMNEdge_flow7">
        <omgdi:waypoint x="589.0" y="127.0"></omgdi:waypoint>
        <omgdi:waypoint x="640.0" y="128.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow8" id="BPMNEdge_flow8">
        <omgdi:waypoint x="675.0" y="128.0"></omgdi:waypoint>
        <omgdi:waypoint x="700.0" y="127.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow9" id="BPMNEdge_flow9">
        <omgdi:waypoint x="1151.0" y="128.0"></omgdi:waypoint>
        <omgdi:waypoint x="1184.0" y="128.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow10" id="BPMNEdge_flow10">
        <omgdi:waypoint x="1224.0" y="128.0"></omgdi:waypoint>
        <omgdi:waypoint x="1269.0" y="128.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow11" id="BPMNEdge_flow11">
        <omgdi:waypoint x="1304.0" y="128.0"></omgdi:waypoint>
        <omgdi:waypoint x="1330.0" y="129.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow6" id="BPMNEdge_flow6">
        <omgdi:waypoint x="355.0" y="127.0"></omgdi:waypoint>
        <omgdi:waypoint x="400.0" y="128.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow5" id="BPMNEdge_flow5">
        <omgdi:waypoint x="505.0" y="128.0"></omgdi:waypoint>
        <omgdi:waypoint x="549.0" y="127.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow47" id="BPMNEdge_flow47">
        <omgdi:waypoint x="250.0" y="147.0"></omgdi:waypoint>
        <omgdi:waypoint x="657.0" y="370.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow48" id="BPMNEdge_flow48">
        <omgdi:waypoint x="569.0" y="147.0"></omgdi:waypoint>
        <omgdi:waypoint x="657.0" y="370.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow50" id="BPMNEdge_flow50">
        <omgdi:waypoint x="675.0" y="387.0"></omgdi:waypoint>
        <omgdi:waypoint x="700.0" y="387.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow51" id="BPMNEdge_flow51">
        <omgdi:waypoint x="805.0" y="387.0"></omgdi:waypoint>
        <omgdi:waypoint x="850.0" y="388.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow52" id="BPMNEdge_flow52">
        <omgdi:waypoint x="890.0" y="388.0"></omgdi:waypoint>
        <omgdi:waypoint x="935.0" y="388.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow53" id="BPMNEdge_flow53">
        <omgdi:waypoint x="970.0" y="388.0"></omgdi:waypoint>
        <omgdi:waypoint x="1015.0" y="388.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow54" id="BPMNEdge_flow54">
        <omgdi:waypoint x="1120.0" y="388.0"></omgdi:waypoint>
        <omgdi:waypoint x="1269.0" y="387.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow56" id="BPMNEdge_flow56">
        <omgdi:waypoint x="45.0" y="128.0"></omgdi:waypoint>
        <omgdi:waypoint x="90.0" y="128.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow57" id="BPMNEdge_flow57">
        <omgdi:waypoint x="195.0" y="128.0"></omgdi:waypoint>
        <omgdi:waypoint x="230.0" y="127.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow59" id="BPMNEdge_flow59">
        <omgdi:waypoint x="569.0" y="147.0"></omgdi:waypoint>
        <omgdi:waypoint x="337.0" y="301.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow60" id="BPMNEdge_flow60">
        <omgdi:waypoint x="320.0" y="318.0"></omgdi:waypoint>
        <omgdi:waypoint x="142.0" y="318.0"></omgdi:waypoint>
        <omgdi:waypoint x="142.0" y="156.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow61" id="BPMNEdge_flow61">
        <omgdi:waypoint x="1204.0" y="148.0"></omgdi:waypoint>
        <omgdi:waypoint x="1203.0" y="318.0"></omgdi:waypoint>
        <omgdi:waypoint x="355.0" y="318.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow63" id="BPMNEdge_flow63">
        <omgdi:waypoint x="836.0" y="127.0"></omgdi:waypoint>
        <omgdi:waypoint x="881.0" y="128.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow64" id="BPMNEdge_flow64">
        <omgdi:waypoint x="921.0" y="128.0"></omgdi:waypoint>
        <omgdi:waypoint x="966.0" y="128.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow67" id="BPMNEdge_flow67">
        <omgdi:waypoint x="1001.0" y="128.0"></omgdi:waypoint>
        <omgdi:waypoint x="1046.0" y="128.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow70" id="BPMNEdge_flow70">
        <omgdi:waypoint x="901.0" y="108.0"></omgdi:waypoint>
        <omgdi:waypoint x="983.0" y="78.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow71" id="BPMNEdge_flow71">
        <omgdi:waypoint x="966.0" y="60.0"></omgdi:waypoint>
        <omgdi:waypoint x="452.0" y="60.0"></omgdi:waypoint>
        <omgdi:waypoint x="452.0" y="101.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow72" id="BPMNEdge_flow72">
        <omgdi:waypoint x="1204.0" y="148.0"></omgdi:waypoint>
        <omgdi:waypoint x="1286.0" y="184.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow73" id="BPMNEdge_flow73">
        <omgdi:waypoint x="1269.0" y="201.0"></omgdi:waypoint>
        <omgdi:waypoint x="898.0" y="200.0"></omgdi:waypoint>
        <omgdi:waypoint x="768.0" y="155.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow74" id="BPMNEdge_flow74">
        <omgdi:waypoint x="1471.0" y="129.0"></omgdi:waypoint>
        <omgdi:waypoint x="1490.0" y="129.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="flow75" id="BPMNEdge_flow75">
        <omgdi:waypoint x="870.0" y="408.0"></omgdi:waypoint>
        <omgdi:waypoint x="870.0" y="481.0"></omgdi:waypoint>
        <omgdi:waypoint x="337.0" y="481.0"></omgdi:waypoint>
        <omgdi:waypoint x="337.0" y="336.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="association1" id="BPMNEdge_association1">
        <omgdi:waypoint x="1319.0" y="71.0"></omgdi:waypoint>
        <omgdi:waypoint x="1286.0" y="111.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="association2" id="BPMNEdge_association2">
        <omgdi:waypoint x="1003.0" y="231.0"></omgdi:waypoint>
        <omgdi:waypoint x="983.0" y="146.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge bpmnElement="association3" id="BPMNEdge_association3">
        <omgdi:waypoint x="1320.0" y="241.0"></omgdi:waypoint>
        <omgdi:waypoint x="1286.0" y="219.0"></omgdi:waypoint>
      </bpmndi:BPMNEdge>
    </bpmndi:BPMNPlane>
  </bpmndi:BPMNDiagram>
</definitions>
```

## Compnent Diagram

```
@startuml

interface IT
interface ops
interface users

component [Clients - APP/Web] as APP
component [Configuration Maintenance - Web] as WEB

ops --> APP
users --> APP
IT --> WEB #blue

package "Server-side" {

	component [API Gateway] as API_GATEWAY #lightgreen

	package "Configuration Center" {
		component [Configuration - Service] as CONF #eee
		database "Configuration DB" as CONF_DB #999
		component [Zookeeper] as ZK #eee

		CONF --> CONF_DB
		CONF --> ZK
	}

	API_GATEWAY ..> CONF #blue

	rectangle "Deployments" {
		cloud "Production Deployment" as PROD  #aliceblue {
		
			rectangle "Production Service Deployment" as PROD_SERVICE {
				component [API - Service] as API << Multiple >>
				component [Queue-based Task Dispatcher] as Q << Single >> #eee
				component [Backend - Service] as BE << Multiple >>
				API --> Q
				Q --> BE
			}

			rectangle "Production Persistance Deployment" {
				package "Production Env" as PROD_DATA {
					component [DB Read Cache] as CACHE #ddd
					database "Core DB" as DB #ddd
					database "Queue DB" as QDB #ddd
				}
				package "Production Sandbox Environment" as SANDBOX_DATA #ddd {
				}
			}

			API --> CACHE
			BE --> DB
			API --> DB
			Q -> QDB

			PROD_SERVICE --> ZK

		}

		cloud "Staging Deployment" as STAGING #aliceblue {
			rectangle "Staging Service Deployment" as STAGING_SERVICE {
			}

			rectangle "Staging Persistance Deployment" as STAGING_DATA #ddd {
			}
			STAGING_SERVICE --> STAGING_DATA
		}

		cloud "Develop Deployment" as DEV  #aliceblue {
			rectangle "Develop Service Deployment" as DEV_SERVICE {
			}

			rectangle "Develop Persistance Deployment" as DEV_DATA #ddd {
			}
			DEV_SERVICE --> DEV_DATA
		}

	}

	API_GATEWAY --> API
	API_GATEWAY ---> STAGING_SERVICE
	API_GATEWAY ---> DEV_SERVICE

}

APP --> API_GATEWAY
WEB --> API_GATEWAY #blue

@enduml
```


## ER Diagram
```
@startuml
package Configuration {
  class Banks #lightgrey {
    Bank Info
    ==
    #id
    ..
    name : varchar(32) not null -- name of bank
    code : varchar(32) not null
    nation : varchar(32) not null
    accountLength : int -- account number length
    validateExpression : varchar(64)
    description : varchar(128) -- desc of bank
  }

  class LoanProducts #lightgrey {
    Loan Products
    ==
    #id
    ..
    +name : varchar(64) -- name of loan product
    amount : decimal(16,2) NOT NULL -- amount of money
    days : int unsigned -- loan days
    preloanFee : decimal(16,2) NOT NULL
    installments : int unsigned NOT NULL -- by stages times
    interestRate : decimal(10,8) NOT NULL -- interest rate
    overdueInterestRate : decimal(10,8) NOT NULL -- overdue interest rate
    minCredit : int unsigned not null -- min credit 
  }
}

class Accounts #cyan {
  Investor & Borrower Accounts
  ==
  #id
  id_Person : bigint unsigned
  id_Certificate : bigint unsigned
  ..
  openId : varchar(128) -- oauth openid
  ..
  +accountName : varchar(128)
  +mobile : varchar(128) not null
  credit : int unsigned not null default 0
  ..
  isDeleted : boolean not null default false
  deletedAt : datetime -- account locked time
  isLocked : boolean not null default false
  lockedAt : datetime -- account locked time
}

package Wallet {
  class Wallets #pink {
      Wallet storing account balance money
      ==
      #id
    id_Account : bigint unsigned not null
      ..
      balance : decimal(20,6) default 0
    ..
      status : varchar(32)
  }

  class WithdrawOrders {
    Wallet Withdraw Order
    ==
    #id
    id_Account : bigint unsigned not null
    ..
    status : varchar(32)
    ..
    amount : decimal(20,6) default 0
    description : varchar(50)
  }
}

WithdrawOrders --> Accounts : created by 1 account
Wallets --> Accounts : belongs to 1 account

package Profiles {

  class Persons {
    Person Profiles
    ==
    #id
    ..
    firstName : varchar(32)
    middleName : varchar(32)
    lastName : varchar(32)
    nationality : varchar(32)
    gender : varchar(10)
    birthday : date
    placeOfBirth : varchar(128)
    maritalStatus : varchar(32)
    mobile : varchar(16)
    email : varchar(64)
    education : varchar(64)
    ..
    residentialDistrictAddress : varchar(128)
    residentialStreetAddress : varchar(128)
    permanentDistrictAddress : varchar(128)
    permanentStreetAddress : varchar(128)
    ..
    property : varchar(32)
    yearlyFamilyIncome : varchar(32)
    ..
    hasUnrepaidLoan : boolean
    unrepaidLoanAmount : decimal(16,2)
    hasOverdue : boolean
    hasFaceRecognition : boolean
    hasFillCompleted : boolean
    holdCertificateImgUrl : varchar(256)
    socialStatus : varchar(32)
    houseHoldBillAddressImgUrl : varchar(256)
  }

  class Cards {
    Bank card information
    ==
    #id
    id_Account : bigint unsigned
    ..
    isPrimary : boolean
    isValid : boolean
    isExpired : boolean
    ..
    bankAccountName : varchar(32)
    bankAccount : varchar(32)
    bankName : varchar(32)
    bankCode : varchar(32)
    bankNation : varchar(32)
  }
  
  class Relatives {
    Account Relatives
    ==
    #id
    id_Account : bigint unsigned
    ..
    firstName : varchar(32)
    middleName : varchar(32)
    lastName : varchar(32)
    gender : varchar(10)
    mobile : varchar(16)
    birthday : date
    email : varchar(64)
    districtAddress : varchar(128)
    streetAddress : varchar(128)
    company : varchar(64)
    ..
    type : varchar(32)
    relationship : varchar(32)
  }
  
  class Works {
    Work Job information
    ==
    #id
    id_Account : bigint unsigned
    ..
    employeeId : varchar(64)
    workIdImgUrl : varchar(256)
    ..
    company : varchar(32) not null
    occupation : varchar(64) not null
    districtAddress : varchar(128) not null
    streetAddress : varchar(128) not null
    email : varchar(64)
    phone : varchar(64)
    entryDate : date not null
    firstPayDay : int unsigned not null
    secondPayDay : int unsigned
    salary : decimal(16,2) not null
    lastestPayCheckDate : date
    secondLastestPayCheckDate : date
    lastestPayslipImgUrl : varchar(256)
  }
  
  class Certificates {
    Certificates
    ==
    #id
    ..
      hasSocialSecurity : boolean
      ssId : varchar(64)
      ssName : varchar(64)
      ssIssueDate : date
      ssExpireDate : date
      ssImgUrl : varchar(256)
    ..
      hasDriverLicense : boolean
      dlId : varchar(64)
      dlName : varchar(64)
      dlIssueDate : date
      dlExpireDate : date
      dlImgUrl : varchar(256)
    ..
      hasPassport : boolean
      ppId : varchar(64)
      ppName : varchar(64)
      ppIssueDate : date
      ppExpireDate : date
      ppImgUrl : varchar(256)
    ..
      hasTaxIdentification : boolean
      tiId : varchar(64)
      tiName : varchar(64)
      tiIssueDate : date
      tiExpireDate : date
      tiImgUrl : varchar(256)
    ..
      hasUnified : boolean
      uniId : varchar(64)
      uniName : varchar(64)
      uniIssueDate : date
      uniExpireDate : date
      uniImgUrl : varchar(256)
  }
}

Accounts --> Persons : identified by 1 Person
Accounts --> Certificates: has 1 certificate info

Accounts <-- Relatives: belongs to 1 Account
Accounts <-- Cards: belongs to 1 Account
Accounts <-- Works: belongs to 1 Account

class Loans #pink {
  Loans information
  ==
  #id
  orderNo : varchar(64) not null
  id_LendOrder : bigint unsigned not null

  .. status ..
  instanceId : bigint unsigned
  status : varchar(32)

  .. copy from InvestOrders ..

  .. copy from LendOrders ..

  .. copy from BorrowOrders ..

  ..
  dueAt : date
  unpaidInstallments : int unsigned NOT NULL

  .. total ..
  debt : decimal(20,6) default 0
  fee : decimal(20,6) default 0
  interest : decimal(20,6) default 0
  overdueInterest : decimal(20,6) default 0
  sum : decimal(16,2) default 0
  
  .. unpaid ..
  unpaidDebt : decimal(20,6) default 0
  unpaidFee : decimal(20,6) default 0
  unpaidInterest : decimal(20,6) default 0
  unpaidOverdueInterest : decimal(20,6) default 0
  unpaidSum : decimal(16,2) default 0
  
  .. repaid ..
  repaidDebt : decimal(20,6) default 0
  repaidFee : decimal(20,6) default 0
  repaidInterest : decimal(20,6) default 0
  repaidOverdueInterest : decimal(20,6) default 0
  repaidSum : decimal(16,2) default 0
}

class BorrowOrders {
    Borrow order
    ==
    #id
    id_Account : bigint unsigned not null
  orderNo : varchar(64) not null
    ..
  status : varchar(32) not null
  type : varchar(32) not null
    ..
  id_Loan : bigint unsigned
  ..
  amount : decimal(16,2) not null
  ..
  bankName : varchar(32)
  bankAccount : varchar(32)

  ..
  debt : decimal(16,2) -- debt=principal+preloanFee
  principal : decimal(16,2) 
  preloanFee : decimal(16,2) 
    .. copy from LoanProducts ..
  name : varchar(64) -- name of loan product
    purpose : varchar(128)
  days : int unsigned -- loan days
  dueAt : date
  interestRate : decimal(10,8) -- interest rate
  overdueInterestRate : decimal(10,8) -- overdue interest rate
  installments : int unsigned default 1 -- by stages times
  ..
  channel : varchar(32)
  description : varchar(256)
}

Loans -> LendOrders : created by 1 LendOrder

BorrowOrders -> Accounts: belongs to 1 account
BorrowOrders ..> LoanProducts: created from 1 loan product

class Overdues #pink {
  Borrow Order Overdue Tickets
  ==
  #id
  orderNo : varchar(64) not null
  id_Loan : bigint unsigned not null
  id_Account : bigint unsigned not null
  ..
  principal : decimal(20,6) default 0
  fee : decimal(20,6) default 0
  overdueInterest : decimal(20,6) default 0
  interest : decimal(20,6) default 0
  dueAt : date
  overduedAt : date
}

Overdues --> Loans : created by 1 overdued loan

class Repayments #pink {
  Loan Repayments
  ==
  #id
  orderNo : varchar(64) not null
  id_Loan : bigint unsigned not null
  id_Account : bigint unsigned not null
  ..
  amount : decimal(16,2) default 0
  dueAt : date not null
  .. repaid ..
  repaidDebt : decimal(20,6) default 0
  repaidFee : decimal(20,6) default 0
  repaidInterest : decimal(20,6) default 0
  repaidOverdueInterest : decimal(20,6) default 0
  repaidSum : decimal(16,2) default 0

  .. unpaid ..
  unpaidDebt : decimal(20,6) default 0
  unpaidFee : decimal(20,6) default 0
  unpaidInterest : decimal(20,6) default 0
  unpaidOverdueInterest : decimal(20,6) default 0
  unpaidSum : decimal(16,2) default 0

  ..
  channel : varchar(32)
}


class Investments #pink {
  Loan Investments
  ==
  #id
  id_InvestOrder : bigint unsigned not null
  orderNo : varchar(64) not null
  id_Loan : bigint unsigned not null
  id_Account : bigint unsigned not null
  ..
  status : varchar(32)

  ..
  amount : decimal(16,2) -- amount=fee+principal
  fee : decimal(16,2)
  principal : decimal(16,2)
  
  ..
  interest : decimal(16,2) default 0
  dueAt : date not null
}

class InvestOrders {
    Investment order
    ==
    #id
  id_Account : bigint unsigned not null
    id_LendOrder : bigint unsigned not null
    id_BorrowOrder : bigint unsigned not null
  ..
  orderNo : varchar(64) not null
  status : varchar(32) not null
  amount : decimal(16,2) not null
  ..
  bank : varchar(32)
  account : varchar(32)
    ..
  interest : decimal(16,2) default 0
    dueAt : date not null
}

class LendOrders {
  Lend Order
  ==
  #id
  id_Account : bigint unsigned not null
  id_BowrrowOrder : bigint unsigned not null
  ..
  status : varchar(32) not null
}

class RepayOrders {
  Repay Order
  ==
  #id
  id_Account : bigint unsigned not null
  id_Loan : bigint unsigned not null
  ..
  status : varchar(32) not null
}

LendOrders --> Accounts : created by 1 Account

RepayOrders --> Accounts : created by 1 Account

RepayOrders -> Loans : belongs to 1 Loan

Repayments --> RepayOrders : created by 1 RepayOrder

LendOrders --> BorrowOrders : belongs to 1 BorrowOrder

Investments --> InvestOrders : created by 1 InvestOrder

InvestOrders --> LendOrders : invested by 1 LendOrder
InvestOrders --> Accounts: created by 1 investor account
InvestOrders --> BorrowOrders: invest to 1 BorrowOrder

@enduml
```