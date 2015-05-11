var greyHostsNoPortsRemove = function() {
  // Loops through each host from the selected project
  // and changes the status of any gray hosts with no open ports
  // to green
  // 
  // Usage: greyHostsNoPortsRemove();
  // Created by: Dan Kottmann
  // Requires client-side updates: true

  var PROJECT_ID = Session.get('projectId');
  var MODIFIED_BY = Meteor.user().emails[0].address;
  var hosts = Hosts.find({'project_id': PROJECT_ID, 'status': 'lair-grey'}).fetch();
  if(typeof hosts === 'undefined' || hosts.length === 0) {
    console.log("No hosts found");
  } else {
    var c = 0;
    hosts.forEach(function(host) {
      var portCount = Ports.find({'host_id': host._id, 'port': {$gt: 0}}).count();
      if(portCount === 0) {
        c++;
        console.log("Updating: " + host.string_addr);
        Hosts.remove({'_id': host._id});
      }
    });
    console.log(c + " host(s) updated");
  }
};
