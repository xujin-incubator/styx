# Session Affinity (aka Sticky Sessions)

Session affinity is configured on an application-by-application basis. It
allows requests by a client to an application to always be routed to the
same origin. This is also known as "sticky sessions" and is useful in
situations where sessions are not shared between instances.

Our current implementation is cookie-based. For each application configured
to use sticky sessions, the client receives a cookie. The value of the
cookie tells Styx which origin to route to. If the client has no cookie,
an origin will be assigned by the load balancer. Once they have a cookie,
they will be routed to the origin it specifies.

If Styx is unable to route to the specified origin, the load balancer will
choose a new origin, and the client's cookie will be overwritten with
the new value.

The *Session Affinity* is configured per application basis by including
the `stickySession` block into the Backend Service block.

# Configuration

    stickySession:
      enabled: true
      timeoutSeconds: 14321

