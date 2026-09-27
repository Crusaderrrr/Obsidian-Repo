ClassificationPipelineIT
Check the core product works end to end — an investor goes in, the checks run, the right result comes out. Today the individual checks are tested separately but never together.

BatchProcessingIT
Check that an uploaded batch actually gets worked through: records are picked up one at a time, a failure puts the record back rather than losing it, and anything left half-done by a restart is recovered. 

ReclassificationIT
Check investors get re-checked correctly, both when a user asks for it and on the automatic schedule, and that the monthly limit and the cost controls on paid external lookups are respected. 

BatchUploadIT
Check that uploading a file of investors works end to end, and that a bad file leaves nothing half-saved.

AuthenticationFlowIT 
Check who can get into the system and what they can reach once inside: the full sign-in journey including two-factor and lockout, then a sweep confirming each user role can only access what it should.

NfaSearchClientIT
Check we talk to the NFA data provider correctly and cope when it's slow or returns an error.

PostgridClientIT
Same for the Postgrid address service. 

FcaSearchClientIT
Same for the FCA source, which we read off a web page rather than a proper interface — making it the most fragile of the three. 

GrayListWorkflowIT
Check the manual review queue hands each case to one reviewer at a time, releases it if they don't finish, and correctly records the reviewer's decision.

ExportStreamingIT
Check exports produce a complete, correct file and behave properly when they're very large or interrupted.

ExternalBatchIT
Check the second way investors reach us — sent in by a partner system rather than uploaded — works end to end, including sending results back and flagging batches that get stuck. Failures here are visible to the partner rather than to us.

MailSchedulerIT
Check emails are prepared, sent and marked as sent, and that the switches for turning each type off are respected — without sending anything real during the test.