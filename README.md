#include "open62541/open62541.h"

int main() {
    // Initialize the open62541 library
    UA_ServerConfig config = UA_ServerConfig_standard;
    UA_Server *server = UA_Server_new(config);

    // Create a variable node (tag)
    UA_VariableAttributes vAttr = UA_VariableAttributes_default;
    UA_Int32 myTagValue = 42;
    UA_Variant_setScalarCopy(&vAttr.value, &myTagValue, &UA_TYPES[UA_TYPES_INT32]);
    UA_NodeId myTagNodeId = UA_NODEID_STRING(1, "MyTag");
    UA_QualifiedName myTagName = UA_QUALIFIEDNAME(1, "MyTag");
    UA_Server_addVariableNode(server, myTagNodeId, UA_NODEID_NUMERIC(0, UA_NS0ID_OBJECTSFOLDER),
                             UA_NODEID_NUMERIC(0, UA_NS0ID_ORGANIZES), myTagName, UA_NODEID_NULL, vAttr, NULL, NULL);

    // Run the server and update the tag value
    UA_Server_run(server, &running);

    // Clean up and stop the server when done
    UA_Server_delete(server);
    return 0;
}
